# Experience API

## Quick Start
Welcome to Edcast's LRS Framework. This document defines how to record learning activities using xAPIs.

##Prerequisites
Developer needs Credentials provided by this EdCast admin and xAPI endpoint to accept triggers from partner's LMS to record activity on EdCast Learning Record Store(LRS).

##Credentials
EdCast admin will provide ```Authorization token``` needed for the header of each call to the LRS using xAPI.


##LRS xAPI Endpoint
>####API
    POST: http://lrs.edcast.com/data/xAPI/statements
>####Headers
    Authorization: [Authorization token]
    X-Experience-API-Version: 1.0.3,
    Content-Type: 'application/json',
    charset: 'utf-8'

>####Body
    {"actor": {
        "name": "test user12",
     "mbox": "mailto:test12@gmail.com"
      },
      "verb": {
         "id": "http://activitystrea.ms/schema/1.0/complete",
          "display": {
             "en-US": "completed"
          }
      },
      "timestamp": "2017-03-10T03:41:22.788Z",
      "object": {
         "id": "https://www.ht2labs.com/blog/xapi-statement-verb/#.WgnXzkqCz",
           "definition": {
                "name": {
                       "en-US": "[Machine Learning]"
                  },
                  "description": {
                       "en-US": "Play with data and train your machine to predict results"
               },
                  "type": "http://adlnet.gov/expapi/activities/course"
        },
         "objectType": "Activity"
     },
    "result":{
        "Score":{
        "scaled":0.95
      },
      "success":true,
      "completion":true,
      "duration": "PT1234S"
      }
    }




> ###Attributes
<table>
  <tr>
    <th>Property</th>
    <th>Type</th>
    <th>Description</th>
    <th>Required</th>
  </tr>
  <tr id="2.4.s1.table1.row2">
    <td><a href="#actor">actor</a></td>
    <td>Object</td>
    <td>Whom the Statement is about, as an <a href="#agent">Agent</a> or 
      <a href=#group>Group</a> Object.</td>
    <td>Required</td>
  </tr>
  <tr id="2.4.s1.table1.row3">
    <td><a href="#verb">verb</a></td>
    <td>Object</td>
    <td>Action taken by the Actor.</td>
    <td>Required</td>
  </tr>
  <tr id="2.4.s1.table1.row4">
    <td><a href="#object">object</a></td>
    <td>Object</td>
    <td>Activity, Agent, or another Statement that is the Object of the Statement. 
    </td>
    <td>Required</td>
  </tr>
  <tr id="2.4.s1.table1.row5">
    <td><a href="#result">result</a></td>
    <td>Object</td>
    <td>Result Object, further details representing a measured outcome.</td>
    <td>Optional</td>
  </tr>
  <tr id="2.4.s1.table1.row6">
    <td><a href="#context">context</a></td>
    <td>Object</td>
    <td>Context that gives the Statement more meaning. Examples: a team the Actor is 
  working with, altitude at which a scenario was attempted in a flight simulator.</td>
    <td>Optional</td>
  </tr>
  <tr id="2.4.s1.table1.row7">
    <td><a href="#timestamp">timestamp</a></td>
    <td><a href="#timestamps">Timestamp</a></td>
    <td>Timestamp of when the events described within this Statement occurred. Set by the LRS if not provided.</td>
    <td>Optional</td>
  </tr>
</table>

----
>## Actor  

  The Actor defines who performed the action. The Actor of a Statement can be an Agent or a Group. 

    "actor": {
      "name": "test user12",
      "mbox": "mailto:test12@gmail.com"
    }

>## Verb

  The Verb defines the action between an Actor and an Activity. 

    "verb": {
       "id": "http://activitystrea.ms/schema/1.0/complete",
        "display": {
           "en-US": "completed"
        }
    }

List of Verbs EdCast will use to process user’s learning profile

| Verb | ID |
| ------ | ------ |
| created | http://activitystrea.ms/schema/1.0/create |
| assigned | http://activitystrea.ms/schema/1.0/assign |
| started | http://activitystrea.ms/schema/1.0/start |
| consumed | http://activitystrea.ms/schema/1.0/consume |
| completed | http://adlnet.gov/expapi/verbs/completed |
| passed | http://adlnet.gov/expapi/verbs/passed |
| failed | http://adlnet.gov/expapi/verbs/failed |
| up voted | http://id.tincanapi.com/verb/voted-up |
| commented | http://adlnet.gov/expapi/verbs/commented |
| viewed | http://id.tincanapi.com/verb/viewed |
| bookmarked | http://id.tincanapi.com/verb/bookmarked |


>## Object

The Object defines the thing that was acted on. The Object of a Statement can be an Activity, Agent/Group, SubStatement, or Statement Reference. 

    "object": {
       "id": "https://www.ht2labs.com/blog/xapi-statement-verb/#.WgnXzkqCz",
         "definition": {
              "name": {
                     "en-US": "[Machine Learning]"
                },
                "description": {
                     "en-US": "Play with data and train your machine to predict results"
             },
                "type": "http://adlnet.gov/expapi/activities/course"
      },
       "objectType": "Activity"
    }
  
  For more example check this

List of Types EdCast will use to process user’s learning profile


| Type | ID |
| ------ | ------ |
| video | http://activitystrea.ms/schema/1.0/video |
| question | http://activitystrea.ms/schema/1.0/question |
| article | http://activitystrea.ms/schema/1.0/article |
| Course | http://adlnet.gov/expapi/activities/course |
| Objective | http://adlnet.gov/expapi/activities/objective |
| image | http://activitystrea.ms/schema/1.0/image |
| collection | http://activitystrea.ms/schema/1.0/collection |
| bookmark | http://activitystrea.ms/schema/1.0/bookmark |
| comment | http://activitystrea.ms/schema/1.0/comment |
| badge | http://activitystrea.ms/schema/1.0/badge |

**Note:** All verbs and types are case sensitive

>##Result

An optional property that represents a measured outcome related to the Statement in which it is included. Example:
  
    "result":{
        "Score":{
        "scaled":0.95
      },
      "success":true,
      "completion":true,
      "duration": "PT1234S"
      }
    } 

#### Duration Format
| Example | Details |
| ------ | ------ |
| PT4H35M59.14S | Four hours, thirty five minutes and 59.14 seconds. |
| P16559.14S | The same time period as above represented in seconds. |
| P3Y1M29DT4H35M59.14S | A Duration also including years, months and days.|
| P3Y | Approximately three years e.g. completion of a qualification.|
| P4W | Four weeks. Note that weeks cannot be combined with other time periods. 'P4W1D' is not valid.|




>## Context

An optional property that provides a place to add contextual information to a Statement. All "context" properties are optional.

    "context": {
       "registration": "957f56b7-1d34-4b01-9408-3ffeb2053b28",
        "contextActivities":{
        "category":[{        
            "id":"http://adlnet.gov/expapi/activities/assessment",
             "definition": {
              "name": {
                   "en": "Assesment"
              },
              "description": {
                  "en": "A category of course with Assesment."
              }
            }
          },
          {
            "id":"http://adlnet.gov/expapi/activities/objective"
          },
          {
            "id":"http://activitystrea.ms/schema/1.0/audio"
          },
          {
            "id":"http://activitystrea.ms/schema/1.0/video"
                    } ]
           },
        "instructor": {
            "name": "Andrew Downes",
            "account": {
                 "homePage": "http://www.example.com",
               "name": "Andrew Downes"
           }
       }
    }

For more example check  this

>## Timestamp

The time at which the experience occurred.

    "timestamp": "2017-11-10T12:17:00+00:00"

