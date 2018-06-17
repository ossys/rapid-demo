## Intro to RAPiD

RAPiD automates the development of your domain model. The domain model is a way to describe and model real world entities and their relationships. Understanding the system level requirements, identifying domain entities and their relationships help everyone involved understand and stay in sync with the project and requirements.

Everyone knows what Ebay is. We are going to build a simplified Ebay with RAPiD by first developing a domain model and then entering that into RAPiD to create an app. Here is the simplified Domain Model.

![alt tag](https://rapid.io/img/Ebay1.png)

We have 3 objects in this model, a User, Auction and Bid. To keep it simple we are only tracking the User’s first and last names, email and password. We know that for Ebay, each User can start many Auctions. So there is a One-to-Many relationship between User and Auction. Again, for simplicity sake we are going to track item name, reserve price, and end date for the Auction. Also each User can place many bids so once again the User has a One-to-Many relationship with Bid, which in this case is only going to track date of the bid and the bid amount. For Ebay to work though, the bids also have to be tied to the Auction they are being applied to. Since one Auction can have many bids, there is a One-to-Many relationship from Auction to Bid. So lets model this with RAPiD.

This is what we will effectively turn into code with RAPiD. The next section will walk you through the set up process and then build

## Requirements

In order to use RAPiD the only dependency is having git installed. If you need to install git you can click [here](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git) to get instructions.

We are assuming by using a nodeJs tool, you will have node, mongo, bower, and gulp installed. If you don’t know how to do that you should probably learn that first. Start [here](http://nodejs.org).

## Account and Setup

### 1) Creating an account and login

a. Click ‘Sign Up’ in the top right of the Home page navigation bar.

b. Fill out the form and click the ‘Sign Up’ button.

c. You will be taken to the home section of the Dashboard.

### 2) Upload Public Key

Go to the SSH Key Page

![alt tag](https://rapid.io/img/AEGoToKeys.png)

Upload Public Key. If you need help to generate or check if you have a public key, click [here](https://help.github.com/articles/generating-an-ssh-key/).

![alt tag](https://rapid.io/img/AESSHtKey.png)

Return to Home

![alt tag](https://rapid.io/img/AEGoHome.png)

### 3) Create a Proejct

Click Add Project

![alt tag](https://rapid.io/img/AEAddProject.png)

Type your new project's name and click 'Create Project'

![alt tag](https://rapid.io/img/AEProjNameCreate.png)

This is your Project Key that will be put into the system.xml file

![alt tag](https://rapid.io/img/AEProjectKey.png)

## Demo

### 1) Cloning the demo and setting up git

a. First open terminal and move to the directory you wish to put your demo.

b. Clone the demo and move into the demo folder by copying and pasting the following into your terminal and then press enter.
`git clone https://github.com/rapid-io/demo && cd demo`

c. Inside the demo folder is an ‘rapid’ folder containing two files called system.xml and model.xml. Open files in the editor of your choice.

d. In the system.xml file replace the value for the key attribute under the SystemModel element with the Project Key developed and save the file.

![alt tag](https://rapid.io/img/AESystemKey.png)

e. Stage files in git by running `git add –-all` in terminal

f. Commit files in git by running `git commit –m “Project Key added”` in terminal

### 2) Understand Model.xml

This is the model that is built in our demo’s model.xml file.

![alt tag](https://rapid.io/img/Ebay1.png)

Open the xml model.xml in the editor of your choice and you can see how the data is structured. You can look at our Model Definition charts below to see definitions of the attributes and elements. Essentially the Entities or Objects are represented in the xml by <business objects="">and the <attributes>are the attributes tracked within the object. The various settings for each attribute and elements are set as values for attributes in the <attribute>elements. Once you get an idea of the structure go to the next step</attribute></attributes></business>

### 3) Add RAPiD repository to git and get your new code

a. In terminal run `git remote add rapid git@rapid.io:demo.git`

b. Push to RAPiD to by running `git push rapid master` in terminal

c. Watch the Magic

d. Pull your new code by running `git pull rapid master` in terminal

### 4) Check out your new code

a. Check out all the new files in an editor.

b. To run the new code, in the terminal first run `bower install` then run `npm install` and finally run `gulp clean && gulp.`

c. In the browser go to ‘http://localhost:3000/’ to see the landing page.

### 4) Make modifications and rerun.

Now we are going to add a new feature of multiple payment methods for a user. Below is the new domain model for this feature.

![alt tag](https://rapid.io/img/Ebay2.png)

Return to the editor and open model.xml Uncomment out the `<payment method>` business object, save the file , stage and commit the by repeating in terminal

a. `git add –-all`

b. `git commit –m “Payment Method added`

c. `git push rapid master`

d. `git pull rapid master`

e. You just added a new feature of multiple Payment Methods.

### 5) Go out and start creating amazing projects.

# Model Definition

### System.xml                      

| Element | Attribute | Required | Default | Definition |
| ---     | ---       | ---      | ---     | ---        |
| SystemModel                                           |
|         |xmlns      | TRUE     |         | http://www.w3.org/2001/XMLSchema |
|         |xmlns:xsi  | TRUE     |         | http://www.w3.org/2001/XMLSchema-instance |
|         | xsi:schemaLocation  | TRUE   |         | http://rapid.ossys.com http://rapid.ossys.com/systemmodel.xsd |
|         |key        | TRUE     |         |The Project key generated in the dashboard when project created |
|         |api        | TRUE     |         |version of the api you are working with. For now only option is 1 |
| DataSource |||| Database setup. Child of System Model and self closing |
|         |name       | TRUE     |         || datasource name |
|         |type       | TRUE     |         || Type of Database - 'MONGODB2' |
|         |host       | TRUE     |         || host location |
|         |schema     | TRUE     |         || name of schema |
|         |port       | TRUE     |         || port for database connection. Must be positive integer |
|         |username   | TRUE     |         || database username |
|         |password   | TRUE     |         ||database password |
| Project |||| Project Setup. Child of System Model |
|         |name       | TRUE     |         | name of Project |
|         |buildtool  | FALSE    |         | 'GULP' |
|         |basedir    | FALSE    | " "     | Directory specification for model creation if desired |
|         |groupId    | FALSE    | " "     | Used for Maven projects |
| Domain |||| Self Closing element as a child of Project |
|         |name       | TRUE     |         |reference name of a model |
|         |src        | TRUE     |         |file location for the model file - should be 'rapid/model.xml' |
|         |datasource | TRUE     |         |datasource name from above datasource element |
|         |language   | TRUE     |         |'NODEJS' |
|         |namespace  | FALSE    |         |Not used for now |
|         |framework  | FALSE    |         |'EXPRESS' |
|         |orm        | FALSE    |         |'MONGOOSE' |
|         |tester     | FALSE    |         |'MOCHA' |

### Model.xml 
| Element | Attribute | Required | Default | Definition |
| --- | --- | --- | --- | --- |
| Domain Model |
|         |xmlns      | TRUE  |             | http://www.w3.org/2001/XMLSchema |
|         |xmlns:xsi  | TRUE  |             | http://www.w3.org/2001/XMLSchema-instance |
|         |xsi:schemaLocation | TRUE |      | http://rapid.ossys.com http://rapid.ossys.com/systemmodel.xsd |
| Business Object | |||Child of Domain Model. An object tracked in the database |
|         |name       | TRUE  |             |name of object. Will be concatenated together in CamelCase |
|         |comment    | FALSE | " "         | description or comment on object |
|         |concurrent | TRUE  | "TRUE"      | just leave as True |
|         |atomic     | TRUE  | "TRUE"      | just leave as True |
|         |auditable  | TRUE  | "TRUE"      | just leave as True |
| Attribute | |||Child of Domain Model. Maps to a field for an object or table |
|         |name | TRUE | |String naming attribute to be tracked. Must be unique for each business object |
|         |persistent | FALSE | "FALSE" | 'TRUE' or 'FALSE' |
|         |type | FALSE | |Data Type being recorded. Options are 'TEXT', 'NUMBER', 'ENUM'(See Enum element), 'BOOLEAN', 'DATE', 'BINARY' |
|         |minsize | FALSE | "0" | minimum value allowed to be entered |
|         |minsize | FALSE | "0" | minimum value allowed to be entered |
|         |maxsize | FALSE | "0" | maximum value allowed to be entered |
|         |comment | FALSE | |Note on the attribute |
|         |characterset | FALSE | "utf-8 " | Character encoding in database |
|         |required | FALSE | "FALSE" | If the attribute has to be entered to record object in database.'TRUE' or 'FALSE' |
|         |signed | FALSE | "TRUE" | Wether or not the value can be negative. 'TRUE' or 'FALSE' |
|         |default | FALSE | " " | Default value for attribute |
|         |precision | FALSE | "0" | Number of decimal places to limit attribute to. Must be a Non-negative integer |
|         |encryption | FALSE | " " | Type of encryption for attribute in cases such as passwords |
|         |validator | FALSE | " " | RegEx expression for validation. 'Email' for quick email validation |
| Enum | |||Child of Attribute Enum for the attribute |
|         |name      | TRUE |       |name of the enum |
| Enum Reference | |||Child of Attribute Enum referencing another set of enums |
|         |name | TRUE | |Name of attribute referenceing another set of enums in object |
| Relationship | |||Child of Business Object. Must come after Attributes and details relationship between tables or objects |
|         |object | TRUE | |Object that the parent business object has a relationship with |
|         |subjectverb | TRUE | |Represents the behavior or relationship of the 2nd object to the parent Business Object |
|         |objectverb | TRUE | |Represents the behavior or relationship of the parent Business Object to the 2nd object |
|         |bidirectional | TRUE | |Wether objects in a relationship can be accessed from both objects or only one.'TRUE' or 'FALSE' |
|         |type | TRUE | |type of relationship - 'ONE-TO-ONE', 'ONE-TO-MANY', 'MAN-TO-MANY' |
|         |onupdate | FALSE | |Action on update - 'CASCADE' or 'RESTRICT' |
|         |ondelete | FALSE | |Action on delete - 'CASCADE' or 'RESTRICT' |
|         |required | TRUE | "FALSE" | Wether relationship is required. 'TRUE' or 'FALSE' |
|         |multi | TRUE | |'TRUE' or 'FALSE' |
|         |embedded | TRUE | |'TRUE' or 'FALSE' |
| Key | |||Child of Business Object. Sets values as a key that is either unique or indexed. Self closing 'Attribute' element(s) must be included inside Key element with a name to detail which Attributes are being affected and type of data such as 'TEXT' or 'NUMBER' set of enums |
|        |type | TRUE | |Either 'UNIQUE' or 'INDEX' |


### About Us

RAPiD is a product of Open Source Systems. Visit us at [http://www.ossys.com](http://www.ossys.com)

### Reach Us

*   [_Check Us Out On Facebook_](https://www.facebook.com/RapidAppDev)
*   [_Check Us Out On Twitter_](https://www.twitter.com/rapid_io)
*   [_support@rapid.io_](mailto:support@rapid.io)

© RAPiD.io - All Right Reserved
