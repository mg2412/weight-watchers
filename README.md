create table query:-

aws dynamodb create-table --table-name menu_items --attribute-definitions AttributeName=item_id,AttributeType=S AttributeName=item_name,AttributeType=S --key-schema AttributeName=item_id,KeyType=HASH AttributeName=item_name,KeyType=RANGE --provisioned-throughput ReadCapacityUnits=5,WriteCapacityUnits=5

//for order table

aws dynamodb create-table --table-name order --attribute-definitions AttributeName=order_id,AttributeType=S --key-schema AttributeName=order_id,KeyType=HASH --provisioned-throughput ReadCapacityUnits=5,WriteCapacityUnits=5

//--aws dynamodb put-item --table-name order --item '{"order_id": {"S": "order_1"},"item_ids":{"L":[{"S":"item_a","S":"item_b"}]},"order_price":{"S":"it is description"},"item_3d_object":{"S":"3d image"},"item_ingredients":{"S":"ingredients"},"item_price":{"N":"290"},"item_eats":{"S":"veg/non veg"},"item_type":{"S":"muglai.chinese"}}' --condition-expression "attribute_not_exists(item_id)"
//-put item in order table will be done thru step function

insert data:-

aws dynamodb put-item --table-name menu_items --item '{"item_id": {"S": "a"},"item_name":{"S":"first"},"item_description":{"S":"it is description"},"item_3d_object":{"S":"3d image"},"item_ingredients":{"S":"ingredients"},"item_price":{"N":"290"},"item_eats":{"S":"veg/non veg"},"item_type":{"S":"muglai.chinese"}}' --condition-expression "attribute_not_exists(item_id)"


for creating order id:-
CURRENT_DATE=$(perl -e 'use POSIX;print strftime "%d-%m-%Y_%T_%z",localtime time;')
