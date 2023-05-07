# cpt304_assignment2
## Tasks
As a website user, l would like to see a list of public holidays for a selected country.As a website user, l would like to select the area (probably state, province, or city) l amresiding as well as a public holiday from the list so that i can see:
a)-The weather information for the selected public holiday in my area.
b)-The available short-term accommodation rental information for the selected day in my area.

## Note
In terms of weather, it is difficult for us to obtain the weather for a particular festival. For example, today is May 7th, and we cannot predict the weather for Christmas, which is unscientific and meaningless, and there is no such API。The closest API can only predict half a month weather conditions within. If the weather of the festival exceeds half a month, in this case, we use the url request with parameters. The request result will be 400 (Bad Request) or 404 (Not Found). So in this coursework, we changed the weather of the day.

In many APIs, you need to provide many necessary parameters to query the hotel, such as the check-in date, how many people are there, what currency is the payment, how long is the check-out date, and how many rooms are needed. 
Since there is not much information provided by coursework, mock data is used here.
