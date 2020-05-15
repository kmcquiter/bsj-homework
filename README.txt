## In this classwork you will be working with the Boston Software Jobs' application. ##

## What you already have ##

** You are already provided with the starter code. Your started code includes the following:
    - index.js  // Entry point of the code
    - package.json // Information about this project
    - views folder, containing two EJS files (index.ejs, jobs.ejs) 


1. To get started, Run 'npm install' in your Terminal. This will install all the required packages from 'package.json'.


2. In you Terminal. Run 'node index.js'   OR 'nodemon index.js'.    Then go to your browser and visit 'localhost:3000/'
    // You can see that you have a basic page and a GET '/' route that displays information from  'index.ejs'


3. Open Compass DB. Create a new database called 'bsj'. Name the collection 'companies'. You don't have to change anything else.


4. Modify your 'app.listen' function.  When the server is started, create a connection with the MongoDB. 
   We have left comments where you should make those edits.
   Hint:  You will have to install the 'mongodb' package and require it. 


5. On 'localhost:3000/', Click on 'View All Jobs' to go the /jobs page. Using the FORM there, add the following 
    companies to your database. You can COPY/PASE information into the respective fields.

    {
        'company_id': 1,
        'name': 'Actifio', 
        'description': 'Actifio enterprise cloud data management enables thousands of businesses around the world to deliver their data just as they deliver their applications and infrastructure… as a service available instantly, anywhere.',
        'logo': 'https://www.tcv.com/wp-content/uploads/2016/12/TCV_0054_actifio.png'
    }
   
    {
        'company_id': 2,
        'name': 'Agero', 
        'description': 'Agero’s mission is to transform the entire driving experience through an unmatched combination of innovative technology and human-powered solutions.',
        'logo': 'https://www.agero.com/sites/all/themes/agero/images/logo_header.png'
    },

    Your form sends the data to the '/add' route. The route is already present in 'index.js'.  
    You will need to get FORM data, and save that data to the MongoDB using the insertOne() method.
    Upon succes, Print a message saying 'Company Inserted' and use the res.redirect('/jobs') method to take the user back to the jobs page.


6. Open Compass DB and see if your deocuments are added the 'companies' collection.


7. Modify you app.get('/jobs, ....)  route. Use the MongoDB's  .find() method to get all the companies from the 
    database.
   Upon success, use the res.render() method to take the user to jobs.ejs.
   You should also send the companies data retrieved from the database and send it to the jobs.ejs page in a variable called 'all_companies'.



8. Modify your 'jobs.ejs' page. Use the forEach loop to display the name of each company on the page. 

   Hint:  Remember you have already sent companies array in a variable called 'all_companies'   


9. Now, your funtionality to CREATE and Read data should be complete.  Use the FORM on your jobs page to add more 
    companies:

    {
        'company_id': 3,
        'name': 'Akamai', 
        'description': 'Akamai is the global leader in Content Delivery Network (CDN) services, making the Internet fast, reliable and secure for its customers.',
        'logo': 'https://www.akamai.com/us/en/multimedia/images/logo/akamai-logo.png'
    }

    {
        'company_id': 4,
        'name': 'AthenaHealth', 
        'description': 'AthenaHealth partners with hospital and ambulatory customers to drive clinical and financial results. We offer medical record, revenue cycle, patient engagement, care coordination, and population health services.',
        'logo': 'https://www.athenahealth.com/sites/ahcom/themes/ah_theme/assets/images/logo-color.svg'
    }
    
     {
        'company_id': 5,
        'name': 'LogMeIn', 
        'description': 'Simplifying how people interact with each other and the world around them to drive meaningful insight, deeper relationships and better outcomes for all has helped LogMeIn grow to become one of the world’s top 10 SaaS companies with a leadership position in every one of our markets.',
        'logo': 'http://www.codesquad-test.org/bootcamp/LogMeIn_logo.png'
    }
    
    {
        'company_id': 6,
        'name': 'TripAdvisor', 
        'description': 'Tripadvisor helps nearly a half a billion travelers each month make every trip their best trip. Use the Tripadvisor site and app to browse hundreds of millions of reviews and opinions of accommodations, restaurants, experiences, airlines and cruises.',
        'logo': 'https://static.tacdn.com/img2/brand_refresh/Tripadvisor_lockup_horizontal_secondary_registered.svg'
    }

    {
        'company_id': 7,
        'name': 'Wayfair', 
        'description': 'Wayfair is one of the world\'s largest online destinations for the home.',
        'logo': 'http://www.codesquad-test.org/assets/img/wayfair_logo.png'
    }

######################## BONUS

10. Modify your 'jobs.ejs' page.  Now instead of just displaying the name of the company, make it clickable with <a> 
    tags  around it. 
    When the user clicks on a company name, take the user to a page called '/view/COMPANY_ID', where COMPANY_ID is a parameter.
    // Hint: You will need to create a app.get('/view/:company_id') route. In this route use the find method to find the
    // company with the particular ID. You will need to use the query parameters 'find({key: value})'
    // Once you have the company object, take the user to a new page called 'company.ejs'. Here you should display all the information about that company, and also display the logo from the company using the <img> tag


11. Modify your 'company.ejs'. At the bottom of the page, create a link using <a> tage. Name it 'Company is Hiring!'.
    When you click on the link, it should take you to the '/updateCompany/:company_id' route. 
    // Again, you will need to create a new route called app.get('/updateCompany/:company_id'). 
    // In this route, use the updateOne() method of MongoDB to update the company of that particular ID. During this update, you should add a new field to the company called, "hiring" and set the value to 'Yes'.
    // Upon success, redirect the user to '/view/COMPANY_ID', where COMPANY_ID is the id of the company we are working with here. Now, you should also show whether the company is Hiring or not.
    // Hint:  You can use the updateOne method like this -->  updateOne({query}, {  $set: {hiring: 'Yes'} } )


12. Modify your 'company.ejs'. At the bottom of the page, create a link using <a> tage. Name it 'Delete Company'.
    When you click on the link, it should take you to the '/delete/:company_id' route. 
    // You will need to create a new route called app.get('/delete/:company_id'). 
    // In this route, use the deleteOne() method of MongoDB to delete that particular company.
    // Upon success, redirect the user to '/jobs'.