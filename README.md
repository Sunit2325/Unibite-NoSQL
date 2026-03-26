# Unibite-NoSQL
from pymongo import MongoClient
from datetime import datetime
client = MongoClient("mongodb://localhost:27017/")
db = client["unibite_nosql"]
reviews = db["reviews"]
activity_logs = db["activity_logs"]
reviews.delete_many({})
activity_logs.delete_many({})
review_data = [
    {
        "review_id": "R1",
        "customer_id": 1,
        "restaurant_id": 1,
        "restaurant_name": "Pizza Express",
        "order_id": 1,
        "rating": 5,
        "review_text": "Very good pizza and fast delivery.",
        "created_at": datetime.now()
    },
    {
        "review_id": "R2",
        "customer_id": 2,
        "restaurant_id": 2,
        "restaurant_name": "Spice Aroma",
        "order_id": 2,
        "rating": 4,
        "review_text": "Tasty food but delivery was a bit late.",
        "created_at": datetime.now()
    }
]
reviews.insert_many(review_data)
log_data = [
    {
        "log_id": "L1",
        "customer_id": 1,
        "activity_type": "search_restaurant",
        "restaurant_name": "Pizza Express",
        "timestamp": datetime.now(),
        "details": {
            "search_term": "pizza"
        }
    },
    {
        "log_id": "L2",
        "customer_id": 1,
        "activity_type": "place_order",
        "restaurant_name": "Pizza Express",
        "order_id": 1,
        "timestamp": datetime.now(),
        "details": {
            "total_amount": 17.00
        }
    },
    {
        "log_id": "L3",
        "customer_id": 2,
        "activity_type": "place_order",
        "restaurant_name": "Spice Aroma",
        "order_id": 2,
        "timestamp": datetime.now(),
        "details": {
            "total_amount": 15.00
        }
    }
]
activity_logs.insert_many(log_data)
print("Reviews:")
for r in reviews.find():
    print(r)
print("\nLogs:")
for log in activity_logs.find():
    print(log)
