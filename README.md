# python_service
We will deploy and scale our app with docker-compose with the following command:

docker-compose up --build --scale master=2
Docker-compose creates a container with our Nginx server, a container for each of the news and weather services and two instances of our main Api master(server).

We can check if everything is running with:

docker ps --format '{{.Names}}'
We must see the following containers running:

nginx
python_service_master_2
python_service_master_1
python_service_news_1
python_service_weather_1
Now time to check how the load balance works. Open two separate terminals and run:

First:

docker logs python_service_master_1 -f
Second:

docker logs python_service_master_2 -f
Now open Postman or your browser and navigate to http://localhost/news?country=gr or http://localhost/weather?city=amsterdam for example.

We will use the free external apis for weather and news api.openweathermap.org & newsapi.org

If you look at the logs of the first terminal you will see that request was redirected to it.

Refresh or make the request again and you will see that the request will be redirected to the second terminal.. And on and on..

And that’s it!
