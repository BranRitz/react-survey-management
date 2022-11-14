# react-survey-management


Partner Information
-------------------

There will be an endpoint that will return all of the data in the database for a professor regarding survey answers. The service will return this data in JSON format via an http call. 

Example call on the command line:
`curl http://localhost:8080/v1/professor/data/{username}`

So if I wanted the data for myself, a professor, and my username was `bkuritz`, I would call:
`curl http://localhost:8080/v1/professor/data/{username}`

An example result would look like:

```
{
    "professor": "bkuritz",
    "survey_data": {
        "example_survey_1": {
            "status": "open",
            "example_student_1": {
              "How many days do you study": 3,
              "What is your current grade": 82
              }, 
             "example_student_2": {
               "How many days do you study": 7,
               "What is your current grade": 98
              },
          "example_survey_2": {
              "status": "closed"
              "example_student_1": {
                "How many dogs do you have": 3,
                "How many cats do you have": 4,
                },
              "example_student_3: {
                "How many dogs do you have": 0,
                "How many cats do you have": 0,
               },    
       }
}
```

Under survey data, we list each survey by name - so here, we have data for a survey named "example_survey_1" and data for a survey named "example_survey_2". Looking at "example_survey_1" as an example, we see the API returns a status for the survey - open or closed. Then, the survey returns answers provided for each student in JSON format. 

You also filter on survey name and student username.

Example call on the command line for filtering by survey name:
`curl http://localhost:8080/v1/professor/data/bkuritz?survey={survey-name}`

So if I wanted the data for questionnaire "dogs-vs-cats" as a professor, and my username was `bkuritz`, I would call:
`curl http://localhost:8080/v1/professor/data/bkuritz?survey=dogs-vs-cats`

Example result

```
{
    "professor": "bkuritz",
    "survey_data": {
          "dogs-vs-cats": {
              "status": "closed"
              "example_student_1": {
                "How many dogs do you have": 3,
                "How many cats do you have": 4,
                },
              "example_student_3: {
                "How many dogs do you have": 0,
                "How many cats do you have": 0,
               },    
       }
}
```
Example call on the command line for filtering by student username:
`curl http://localhost:8080/v1/{professor username}/data?student={student username}`

So if I wanted the data the student with username "cdavis" has submitted to all of my questionnaire, and my professor username was `bkuritz`, I would call:
`curl http://localhost:8080/v1/bkuritz/data?student=cdavis`

Example result

```
{
    "professor": "bkuritz",
    "survey_data": {
        "example_survey_1": {
            "cdavis": {
              "How many days do you study": 3,
              "What is your current grade": 82
              }, 
          "example_survey_2": {
              "cdavis": {
                "How many dogs do you have": 3,
                "How many cats do you have": 4,
                },

       }
}
```

In order to access this API call, you'll have to run it locally. Ideally, this would be an http call to a webpage on the internet, but this MVP will likely not be hosted by the end of this course. Instead, 

1. Clone this repo.
2. On the command line, move into the top level directory of the repo. You should see a "Dockerfile" and "docker-compose.yml" file. 
3. Run `pip install -r requirements.txt` to install all required 
4. Run `docker-compose up -d`, which will spin up all services for this project as daemons.
5. You can now run the above commands on the ommand line to hit the services. 
6. For your project, you can use whatever requests library to send http requests to this service. 
7. From here, you should be able to use a library to return a CSV file from the returned JSON of these http requests. 

                
      
