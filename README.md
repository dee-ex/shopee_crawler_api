# Shopee Crawler API
It is an API helps you crawl data from https://shopee.vn/ about **brands** & **products** and save them to database which you can access later by also this one.
# Usage
Fistly, we have to care about database migration. Supposed you're a MySQL user then:
```
migrate -database "mysql://username:password@tcp(yourhost:port)/databasename" -path migrations up
```
By `migrations` folder, you can easily `up` and `down`.  
Secondly, you need to config database in `env\database.env`. Here is an example:
```
DATABASE_CONFIGURED = "YES"
DATABASE_USERNAME = "MY_USERNAME"
DATABASE_PASSWORD = "MY_PASSWORD"
DATABASE_HOST = "LOCALHOST"
DATABASE_PORT = "9998"
DATABASE_MAINDATABASENAME = "MAIN"
DATABASE_TESTDATABASENAME = "TEST"
```
Lastly, run the server:
```
go run .
```
Running port is changeable in `env/server.env`.
# Test
Use the following commands:
```
go test github.com/dee-ex/shopee_crawler_api/modules/brands
go test github.com/dee-ex/shopee_crawler_api/modules/products
```
# Route Details
## Crawl Brands
Crawl all brands from https://shopee.vn/mall/brands.
```
/jobs/trigger/crawl_brands
```
## Crawl Products
Crawl all products from https://shopee.vn/username. Can adjust by query parameters.
```
/jobs/trigger/crawl_products?limit=X&from=Y&to=Z
```
## Endpoint `brands`
### Create a Brand (POST)
```
/brands
```
Create a new brand from data containing in body of request, save it to database and return as JSON.
```
{
    "Shopid": 999999,
    "Username": "testusername",
    "BrandName": "testbrandname",
    "Logo": "testlogo"
}
```
### Get All Brands (GET)
```
/brands
```
Get all brands and return as JSON.
### Get Detail a Brand (GET)
```
/brands/{brand_id}
```
Get detail a brand by ID and return as JSON.
### Update a Brand (PUT)
```
/brands/{brand_id}
```
Update a brand by ID. Updated data containing in body of request. Arguments are not required.
```
{
    "BrandName": "updatebrandname",
    "Logo": "testlogo"
}
```
### Delete a Brand (DELETE)
```
/brands/{brand_id}
```
Delete a brand by ID.
### Get All Products of a Brand (GET)
```
/brands/{brand_id}/products
```
Get all products of a specific brand and return as JSON.
## Endpoint `products`
### Create a Product (POST)
```
/products
```
Create a new product from data containing in body of request, save it to database and return as JSON.
```
{
    "Shopid": 999999
    "Itemid": 999998
    "PriceMax": 999997
    "PriceMin": 999996
    "Name": "testname"
    "Images": "testimage"
    "HistoricalSold": 999995
    "Rating": "testrating"
}
```
### Get All Products (GET)
```
/products
```
Get all products and return as JSON.
### Get Detail a Product (GET)
```
/products/{product_id}
```
Get detail a product by ID and return as JSON.
### Update a Product (PUT)
```
/products/{product_id}
```
Update a product by ID. Updated data containing in body of request. Arguments are not required.
```
{
    "Shopid": 999994
    "PriceMax": 999993
    "PriceMin": 999992
    "Name": "updatename"
    "Images": "updateimages"
    "HistoricalSold": 999991
    "Rating": "updaterating"
}
```
### Delete a Product (DELETE)
```
/products/{product_id}
```
Delete a product by ID.