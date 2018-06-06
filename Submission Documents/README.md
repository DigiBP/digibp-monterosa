# FHNW School of Business Onboarding Process #

Authors: Fabian Feiler, Lia Flück, Daniel Horn, Puneeth Krishna Suresh, Daniel Werner

digibp-monterosa


## Introduction ##


### Motivation ###

All students of the FHNW School of Business have gone through one big decision. What is the optimal degree program for one's interests, skills and career prospective? What are the differences and specialties of the different programs? What are the basic criteria for a program? Many students have given feedback that they wish more support of these decisions from the school. The sub-process **Recommend Study Program** of the overall **FHNW School of Business Onboarding Process** solve this problem by providing a digitized workflow that leads students interactively through finding the answers to these questions.

As one of the group members of the digibp-monterosa team works for the FHNW School of Business and is the project manager of the digitalization project of the sub-process **program registration** this is the perfect opportunity to introduce the new sub-process **Recommend study program**.


### Vision ###

Matching a prospective student with the best fitting study program to foster the potential and satisfaction for students, study program, class environment and, therefore, as a consequence the society in economic and cultural aspects.


### Project Organization ###

The project **digitalization of the FHNW School of Business Onboarding Process** is split into two sub-projects. The program registration project is managed within the FHNW School of Business organization. Its planned go-live is in spring 2019 and includes an online registration of the program through the tool ONLA that closely connected to EVENTO, the school's student management system. The sub-project **recommend study program** is implemented within the module **Digitalization of Business Processes** within the MSc Business Information Systems program. The project goal is the implementation of a workflow management system that supports students to decide for a study program that matches their skills and preferences. This sub-project is implemented within the spring semester 2018. In the following project overview, the outline of the sub-project is shown. The implementation of certain parts goes in line with the lectures in the module. 

![alt text](https://github.com/DigiBP/digibp-monterosa/blob/master/Submission%20Documents/Images/Organisation.PNG)


## Process ##
### Process Description ###

The overall process that is digitized within this module is the **FHNW School of Business Onboarding Process**. 
This process includes two sub-processes, the **Recommend Study Program process** and the **Program Registration Process**. 
As the **Program Registration process** is being digitized within an ongoing project by the School of Business, 
the main focus in this module lies on the **Recommend Study Program process**.

![alt text](https://github.com/DigiBP/digibp-monterosa/blob/master/Submission%20Documents/Images/Processes.PNG)


The FHNW school of Business Onboarding Process leads potential students of the School of Business from the first interest in being a student to the actual admission in a program (in a first step only BSc programs). In the sub-process **Recommend Study Program process**, the interested person is supported in choosing a program that matches his/her skills, interests and life-style. Also, the person can then participate in tests that enforce his/her choice. As soon as the interested person decides to register for the recommended program, the second sub-process, the **Program Registration process**, is triggered. 

Sub-Process: **Recommend Study Program Process**
- Process Goals: Support prospective students in their program decision, eliminate programs from the choice that do not meet the basic requirement for the person (does not meet language requirement, does not meet requirement for full-time/part-time program), 
- Inputs: form "Possibility Questionnaire", form "Recommendation Questionnaire", discretionary tasks (Loop) "Skills Tests"
- Outputs: List of possible programs, list of program recommendations, test results

Sub-Process: **Program Registration**
- Process Goals: Registration for program, check eligibility, payment of registration fee, add profile to EVENTO, discretionary task: interview
- Inputs: form "Program Registration", submit required documents (not digital), registration fee payment
- Outputs: program registration


"Recommend Study Program" as-is process:
Currently, there is only the sub-process "Program Registration" existent. There is no support for prospective students to decide for a program. As the overall onboarding process is going through some changes and digitalization efforts, this is a good moment to re-design the process and add the sub-process of program recommendations. 


Project "Recommend Study Program":
The project for the digitalization of the sub-process "Recommend Study Program" is done within the Module "Digitalization of Business Processes" of the MSc Business Information Systems program. The goal is to digitize the process through a workflow management system with some service integration.


### Process Modell ###

The following picture illustrates the complete designed process:

![alt text](https://github.com/DigiBP/digibp-monterosa/blob/master/Submission%20Documents/Images/Process_Camunda.png)

The process starts with the prospective candidate, that visits the created WordPress website and clicks on the study recommendation 
link. This link forwards the user to the first google-form where 

#### Task Types ####
![alt text](https://github.com/DigiBP/digibp-monterosa/blob/master/Submission%20Documents/Images/Task_types.png)

#### Event Types ####
![alt text](https://github.com/DigiBP/digibp-monterosa/blob/master/Submission%20Documents/Images/event_types.png)

#### User & Groups ####
![alt text](https://github.com/DigiBP/digibp-monterosa/blob/master/Submission%20Documents/Images/User.png)



## Digitalization ##
### DMN ###

Within the first process step according to the process model, a user is going to fill in a questionnaire. Based on the input data of this questionnaire and the [study regulation](https://www.fhnw.ch/de/studium/wirtschaft) a preselection of possible study programs is made by a DMN (Decision Model and Notation). The following DRD (Decision Requirement Diagram) shows the relation of the input data for the DMN.

![alt text](https://github.com/DigiBP/digibp-monterosa/blob/master/Submission%20Documents/Images/DRD_BSc_program.png)

The determined business rules have been applied within a DMN in order to execute a preselection of a study program. The following DMN shows the determined business rules.

![alt text](https://github.com/DigiBP/digibp-monterosa/blob/master/Submission%20Documents/Images/DMN_BSc_program.png)

### Services ###

The following services have been implemented into the process:
- Google Forms combined with a WordPress Website
- Google Sheets
- Chatbot

Due to user friendliness, the Chatbot has not been connected. Instead Google Forms and Google Sheets have been connected to the process.

#### Google Forms / WordPress Website ####

As simple WordPress website has been created which is combined with Google Forms (see [URL](https://programrecommendation.wordpress.com)). This Website serves as a starting point of the process. The Google Forms has been linked with responses in a Google Sheet. Google sheets runs a script when the Google Form is submitted ([see script](https://github.com/DigiBP/digibp-monterosa/blob/master/Submission%20Documents/txt/Google_Sheets_rest_API_camunda.txt)). The script triggers the process to be started. The first Task in the process is a Service Task, sending an e-mail to the user with the camunda invitation link.

#### Google Sheets ####

Within the process step "fill in recommendation questionnaire" of the process model a user is going to fill in form. The data from this form is posted in a Google Sheets file. The objective of the Google sheet is to calculate the best match of a study program. The following image shows a screenshot of the Google Sheet. 

![alt text](https://github.com/DigiBP/digibp-monterosa/blob/master/Submission%20Documents/Images/excel.png)

Logic of the Google Sheet:
1. Camunda values are posted in column B [Questionnaire form data]
2. For each Bachelor program, an ideal questionnaire-response was defined in relation with program heads.
3. The prospective candidate’s questionnaire result is then compared to these pre-defined responses.
4. Ranking is based on “Olympic Medal-Model”:
     -	highest number of perfect matches
     -	in case of tie: higher number of only one deviation
     -	in case of tie: higher number of only two deviations
     -    and so on
     
     Same Logic for second and third matches
5. In the cells A36 to B38 an output containing the 3 best matches of study programs will be displayed.

#### Chatbot ####

An initial effort of providing a more personalized function is provided to capture the preliminary details using a chat bot. This scenario is realized using Dialog Flow and Integromat. The values are stored in Spreadsheet using web hooks.

A brief description of the concept used to realize this is depicted below:

- The Different Intents created and used to realize this Chat bot are shown below
![alt text](https://github.com/DigiBP/digibp-monterosa/blob/master/Submission%20Documents/Images/chatbot1.png)

- The Chat bot is triggered when the candidates provides “hi” or “hello” as a greeting message and the flow of communication is passed to the next intent. The concept used in creating this is an inline intent within the context of the existing intent as shown below:
![alt text](https://github.com/DigiBP/digibp-monterosa/blob/master/Submission%20Documents/Images/chatbot2.png)

- The entities in this case were Boolean values (yes or no), thus this example did not used any inbuilt entity and created four different entities for the Boolean values that we require.
![alt text](https://github.com/DigiBP/digibp-monterosa/blob/master/Submission%20Documents/Images/chatbot3.png)

- The value at each intent is captured and stored for that instance and passed on to the next so that at the end of the entire conversation, a combination of all captured values can be collected and passed on to Integromat for back end service integration (In our example a Google spreadsheet). An example of both the above-mentioned scenarios are shown below:

![alt text](https://github.com/DigiBP/digibp-monterosa/blob/master/Submission%20Documents/Images/chatbot4.png)

![alt text](https://github.com/DigiBP/digibp-monterosa/blob/master/Submission%20Documents/Images/chatbot5.png)

-Since this example demonstrated an inline intent, it is not required to enable a web-hook to call for each intent. The web hooks need to be enabled in Dialog Flow where the values of all the intents (Ex: Last Intent) is being captured as shown below:
![alt text](https://github.com/DigiBP/digibp-monterosa/blob/master/Submission%20Documents/Images/chatbot6.png)

- A scenario has to be created in integromat to capture the values from Dialog Flow and store it in the back end. This example demonstrates a simple example of web hooks and Google Spreadsheet as shown below:

![alt text](https://github.com/DigiBP/digibp-monterosa/blob/master/Submission%20Documents/Images/chatbot7.png)

- This has to be connected with Dialog Flow using a Web hooks URL and pasted in the Fulfilment stage of Dialog Flow.

- Once this step is completed and run for a demo, all values communicated and captured in the chat bot would be sent to the Web hooks and in turn to each individual row on Google Spreadsheet as shown below:

![alt text](https://github.com/DigiBP/digibp-monterosa/blob/master/Submission%20Documents/Images/chatbot8.png)

![alt text](https://github.com/DigiBP/digibp-monterosa/blob/master/Submission%20Documents/Images/chatbot9.png)

### Integration ###

For the integration of the services Microsoft Flow and Integromat have been used.

#### Microsoft Flow ####

##### Microsoft Flow – POST: Sending of information e-mail 

Microsoft flow has been used for sending an e-mail containing information concerning the study program (after gateway of process step "Chose netx steps").

- Service Task REST with Body
- URL: [MS Flow HTML request]
- Method: POST
- Headers: Content-Type:application/json
- Payload: 

var email = execution.getVariable("email");
var out = {"email":email};
JSON.stringify(out);

![alt text](https://github.com/DigiBP/digibp-monterosa/blob/master/Submission%20Documents/Images/Post_sending_email.png)

[Link JSON-Request](https://github.com/DigiBP/digibp-monterosa/blob/master/Submission%20Documents/txt/JSON_request_sending_mail.txt)

##### Microsoft Flow – POST: Sending of invitation e-mail

An e-mail is going to be send to the user containing the camunda invitation link (process step "Invite candidate to Camund").

- Service Task REST with Body
- URL: [MS Flow HTML request]
- Method: POST
- Headers: Content-Type:application/json
- Payload: 

var email = execution.getVariable("email");
var out = {"email":email};
JSON.stringify(out);

![alt text](https://github.com/DigiBP/digibp-monterosa/blob/master/Submission%20Documents/Images/post_sending_email_invitation.png)

[Link JSON-Request](https://github.com/DigiBP/digibp-monterosa/blob/master/Submission%20Documents/txt/JSON_request_sending_mail_invitation.txt)

##### Microsoft Flow – POST Questionnaire Data to Google Sheets

Microsoft Flow has been applied in order to post the input data from the questionnaire to the Google Sheets.

- Service Task REST with Body
- URL: [MS Flow HTML request]
- Method: POST
- Headers: Content-Type:application/json
- Payload: form field variables


![alt text](https://github.com/DigiBP/digibp-monterosa/blob/master/Submission%20Documents/Images/MS_flow_1.png)
...
![alt text](https://github.com/DigiBP/digibp-monterosa/blob/master/Submission%20Documents/Images/MS_flow_2.png)


JSON-Request to post the data looks as follow:

[Link JSON-Request](https://github.com/DigiBP/digibp-monterosa/blob/master/Submission%20Documents/txt/JSON_request_MS_flow.txt)

#### Integromat ####

##### Integromat – GET program recommendation from Google Sheets 

Integromat has been appllied in order to get the study recommendation from Google Sheets.

- Service Task REST without Body
- URL: [Integromat webhook]
- Method: GET

![alt text](https://github.com/DigiBP/digibp-monterosa/blob/master/Submission%20Documents/Images/Integromat.png)

The JSON for request the data looks as follow:

![alt text](https://github.com/DigiBP/digibp-monterosa/blob/master/Submission%20Documents/Images/Integromat_JSON.png)

The same applies for “second” and “third” program. Both invoked separately by an own integromat scenario.

## Step by step Instruction ##

1. Press on [this link](https://programrecommendation.wordpress.com) to start the process and land on the WordPress website.

2. On the WordPress website press on "Click here!"
![alt text](https://github.com/DigiBP/digibp-monterosa/blob/master/Submission%20Documents/Images/1.website.png)

3. Fill in the form. It is important to enter a valid e-mail address, otherwise there is no possibility to send you an e-mail.
![alt text](https://github.com/DigiBP/digibp-monterosa/blob/master/Submission%20Documents/Images/2.fill_in_the_form.png)

![alt text](https://github.com/DigiBP/digibp-monterosa/blob/master/Submission%20Documents/Images/2.fill_in_the_form2.png)

4. Finally send the form.
![alt text](https://github.com/DigiBP/digibp-monterosa/blob/master/Submission%20Documents/Images/2.fill_in_the_form3.png)

5. Check your mail inbox, there you find the following mail. Click on the link in the mail.
![alt text](https://github.com/DigiBP/digibp-monterosa/blob/master/Submission%20Documents/Images/3.Mail_inbox.png)

6. Login to Camunda 
![alt text](https://github.com/DigiBP/digibp-monterosa/blob/master/Submission%20Documents/Images/4.camund_sign_in.png)

7. Click on "Check data" in the Camunda and a form appears with the data submitted via the form in step 3. Check the data and click on complete at the bottom right.
![alt text](https://github.com/DigiBP/digibp-monterosa/blob/master/Submission%20Documents/Images/5.camunda_check_data.png)

8. Click on "Show BSc Programs and decide"
![alt text](https://github.com/DigiBP/digibp-monterosa/blob/master/Submission%20Documents/Images/6.show_BSC.png)

9. Based on the input transmitted via the form in step 3, a first recommendation of study program is displayed. For further procedure, click on "Complete".
![alt text](https://github.com/DigiBP/digibp-monterosa/blob/master/Submission%20Documents/Images/7.first_recommendation.png)

10. Know click on the task "Fill in recommendation questionnaire". Fill in the form and press on complete.
![alt text](https://github.com/DigiBP/digibp-monterosa/blob/master/Submission%20Documents/Images/8.Fill_in_recommendation_questionnaire.png)

11. Based on the input given via the form in step 10, the first three best matches are going to be displayed. 

First the best match is going to appear. Then click on "Complete".
![alt text](https://github.com/DigiBP/digibp-monterosa/blob/master/Submission%20Documents/Images/9.first_match.png)

Then the second match. Then click on "Complete".
![alt text](https://github.com/DigiBP/digibp-monterosa/blob/master/Submission%20Documents/Images/10.second_match.png)

And finally, the third match. Then click on "Complete".
![alt text](https://github.com/DigiBP/digibp-monterosa/blob/master/Submission%20Documents/Images/11.third_match.png)

12. Finally, the next step can be chosen.
![alt text](https://github.com/DigiBP/digibp-monterosa/blob/master/Submission%20Documents/Images/12.next_step.png)

13. Afterwards an e-mail has been sent with the corresponding information, depending on the choice made in step 12.
![alt text](https://github.com/DigiBP/digibp-monterosa/blob/master/Submission%20Documents/Images/13.confirm-mail.png)

14. There should be an e-mail in your inbox. When selected in step 12. "I would like to receive the application form", the following link with the application form is going to be in your inbox. At this point the process ends.
![alt text](https://github.com/DigiBP/digibp-monterosa/blob/master/Submission%20Documents/Images/14.mail_inbox_documents.png)
