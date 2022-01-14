# API-TESTING
Base_Url: https://restful-booker.herokuapp.com
#########################################################################################################################
Create Requests: 
Method Type : GET
url: Base_Url/booking/id
 
 Body: 
 {
	"firstname" : "Masud",
	"lastname" : "Parvez",
	"totalprice" : 111,
	"depositpaid" : true,
	"bookingdates" : {
    	"checkin" : "2018-01-01",
    	"checkout" : "2019-01-01"
	},
	"additionalneeds" : "Breakfast"
}

 Response:
 {
    "bookingid": 19,
    "booking": {
        "firstname": "Masud",
        "lastname": "Parvez",
        "totalprice": 111,
        "depositpaid": true,
        "bookingdates": {
            "checkin": "2018-01-01",
            "checkout": "2019-01-01"
        },
        "additionalneeds": "Breakfast"
    }
}
########################################################################
Tests:
var jasonData = pm.response.json()
pm.environment.set("id",jasonData.bookingid)

pm.test("Status code is 200", function () {
    pm.response.to.have.status(200);
});

Tests Results:
  Status code is 200
#######################################################################################  
Get Request: Method - POST
  body: 
    {
	"firstname": "Sally",
	"lastname": "Brown",
	"totalprice": 111,
	"depositpaid": true,
	"bookingdates": {
    	"checkin": "2013-02-23",
    	"checkout": "2014-10-23"
	},
	"additionalneeds": "Breakfast"
}
###############################################################################################
Auth-Token Request: 
Method:POST 
url:{{url}}/booking/{{id}}
body:
    {
	"firstname" : "@@@//..,+",
	"lastname"  : "Uddin",
	"totalprice" : 111,
	"depositpaid" : true,
	"bookingdates" : {
    	"checkin" : "2018-01-01",
    	"checkout" : "2019-01-01"
	},
	"additionalneeds" : "Breakfast"
  
  body: 
    {
	"username": "admin",
	"password": "password123"
}

Tests :
  pm.test("Succesful request", function () {
    pm.response.to.have.status(200);
});
pm.test("Not Found", function () {
    pm.response.to.have.status(404);
});
############################################################################################################
Delete Requests :
  Cookie : token={{accessToken}}
  
Tests :
pm.test("201: Data eleted Successfully!", function () {
    pm.response.to.have.status(201);
});

Response: Created
