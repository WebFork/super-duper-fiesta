```
import json
import boto3

def lambda_handler(event, context):
    phone = event['Details']['ContactData']['CustomerEndpoint']['Address']
    dynamodb = boto3.resource('dynamodb')
    table_name='CustomerDT'
    table = dynamodb.Table(table_name)
    item_key={'PhoneNumber': phone}
    response = table.get_item(Key=item_key)
    
    if 'Item' in response:
        item = response['Item']
        return {
            'Name': item['CustomerName'],
            'Address': item["Address"]
        }
        
    return {
        'statusCode': 200,
        'Name': "John Doe"
        ""
    }
