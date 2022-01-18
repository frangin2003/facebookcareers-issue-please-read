# facebookcareers, sharing some feedback on an issue I faced
Been facing some issues while completing the facebookcareers resume for a job application, sharing my findings.


While I was completing my resume for the job offer "Director, Product Technical Program Management", I have been encountering some issues so I am sharing findings.
While completing a work description in my resume, I got this error message in the form:
![image](https://user-images.githubusercontent.com/6178886/149855534-7357220a-2dcf-4ec4-a610-12ba385b8605.png)

At first, I was wondering if I was using some unauthorized characters, so I have been digging a bit in the source code of the web page:
![image](https://user-images.githubusercontent.com/6178886/149855056-9187e02c-5677-4915-a727-5769a52c65b7.png)

I found that there is a validation function in CareersV2RefreshJobApplicationValidationHelper named checkRegexValidity, that, amongst other checks, verifies that "workDescription" is not breaking a 1000 characters maximum limitation:
![image](https://user-images.githubusercontent.com/6178886/149855409-670fa9be-bf29-4e96-b289-f209e09c56ff.png)


My humble recommandation would be to give a better feedback to the users, so they understand why the description is not valid.

To ease my edit, I have injected some code using a conditional breakpoint:
![image](https://user-images.githubusercontent.com/6178886/149856515-12bdde0c-e53c-4097-a635-a25f6761a1b1.png)

Since the condition is never met (there is indeed no condition to meet), application is not halting but printing the number of characters remaining and if I am breaking the limit:
![image](https://user-images.githubusercontent.com/6178886/149856665-5ddcae04-2eee-4319-8233-83e2833f1e92.png)

## BONUS
I have enhanced a bit the use of conditional breakpoint by additionally setting a global variable with a clearer error message and replacing the error message in the form:
![image](https://user-images.githubusercontent.com/6178886/149857268-16b8e10e-8ca0-4bfa-b162-ab71a7b18e7d.png)

I found the method setting the error message:
![image](https://user-images.githubusercontent.com/6178886/149858193-3a4797cb-084e-41a9-b5ae-21f8d8b675f1.png)

Then I have injected in function updateQuestionError some code to replace the error message by my character count (using false to avoid that the conditional breakpoint halts)
![image](https://user-images.githubusercontent.com/6178886/149858001-efbcca4e-20e8-4958-978b-e020e3b4c404.png)

Now  I have a better feedback:
![image](https://user-images.githubusercontent.com/6178886/149858301-f1e7ff85-a2b7-4909-b1d5-ccf1a9b21d4d.png)
