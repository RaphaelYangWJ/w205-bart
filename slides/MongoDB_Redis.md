
# MongoDB 



1. **Real-time Data Processing**: MongoDB provides fast read and write operations, making it suitable for real-time data processing. As drones deliver packages and transmit information, MongoDB can handle the incoming data quickly, enabling real-time monitoring and analysis of the delivery process.
2. **Scalability**: BART Stations are likely to have a vast number of drones, deliveries, and station-related data to manage. MongoDB's horizontal scalability allows the system to handle increasing data volumes and concurrent users efficiently.
3. **Rich Query Language**: MongoDB's expressive query language allows complex queries and aggregations, enabling the company to derive valuable insights from the data. They can analyze delivery patterns, identify bottlenecks, and optimize delivery routes using MongoDB's querying capabilities.
4. **Internet of Things (IoT) Support**: MongoDB's support for IoT applications makes it an ideal choice for integrating with drones and other IoT devices. This allows seamless data exchange between the drones and the backend system, enabling real-time tracking and management.

## MongoDB Codes: Data Model Design and Inserting Data

```python
import pymongo

client = pymongo.MongoClient('mongo_db_connection')
db = client['delivery_system_db']

# Collection for BART Stations
stations_collection = db['stations']
station_data = {
    'name': 'Station A',
    'location': {'type': 'Point', 'coordinates': [longitude, latitude]},
    # Other station-specific data
}
stations_collection.insert_one(station_data)

# Collection for Drones
drones_collection = db['drones']
drone_data = {
    'name': 'Drone 001',
    'status': 'idle',  # or "in transit"
    'currentLocation': {'type': 'Point', 'coordinates': [longitude, latitude]},
    # Other drone-specific data
}
drones_collection.insert_one(drone_data)

# Collection for Deliveries
deliveries_collection = db['deliveries']
delivery_data = {
    'orderId': '12345',
    'packageWeight': 1.5,  # in kg
    'packageSize': 'medium',
    'destination': {'type': 'Point', 'coordinates': [longitude, latitude]},
    'status': 'pending',  # or "in progress" or "completed"
    'assignedDrone': 'Drone 001',
    # Other delivery-specific data
}
deliveries_collection.insert_one(delivery_data)

```



# Redis

1. **In-memory Data Store**: Redis is an in-memory data store, meaning it stores data in RAM. This allows for extremely fast read and write operations, making it ideal for real-time data processing, which is essential for tracking drones and deliveries in real-time.
2. **High Performance**: Redis is designed for high-performance scenarios and can handle a massive number of operations per second. This capability is crucial in a delivery system with drones, where thousands of drones may be updating their locations and statuses simultaneously.
3. **Pub/Sub Messaging**: Redis supports Publish/Subscribe messaging, allowing drones to publish their status updates to specific channels. Clients can subscribe to these channels to receive real-time updates about drone movements and delivery statuses, enabling real-time tracking of deliveries.
4. **Geospatial Indexing**: Redis has native support for geospatial indexing, which allows the company to store and query spatial data efficiently. This is essential for tracking drone locations, monitoring delivery destinations, and optimizing drone routes based on real-time conditions.
5. **Caching**: Redis can be used as a cache to store frequently accessed data, such as delivery routes or frequently requested delivery information. Caching can significantly reduce the response times and improve overall system performance.
6. **Real-time Analytics**: Redis supports various data structures and commands that enable real-time analytics. Companies can use Redis to aggregate and analyze delivery data on-the-fly, allowing them to make data-driven decisions to improve delivery efficiency.
7. **Distributed Architecture**: Redis can be deployed in a distributed manner using Redis Cluster or Redis Sentinel, providing high availability and fault tolerance. This ensures the delivery system remains robust and operational even in the event of node failures.

## MongoDB Codes: Tracking Delivery Status

```python
import redis

redis_client = redis.StrictRedis(host='redis_host', port=your_redis_port, decode_responses=True)

# Storing delivery status in Redis
def update_delivery_status(order_id, status):
    redis_client.hset('delivery_status', order_id, status)

# Retrieving delivery status from Redis
def get_delivery_status(order_id):
    return redis_client.hget('delivery_status', order_id)

# Example usage:
order_id = '12345'
status = 'in progress'
update_delivery_status(order_id, status)

# Later, retrieve the status:
delivery_status = get_delivery_status(order_id)
print(delivery_status)
```

