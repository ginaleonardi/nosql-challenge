
  <h3>Instructions</h3>
  <p>The UK Food Standards Agency evaluates various establishments across the United Kingdom, and gives them a food hygiene rating. You've been contracted by the editors of a food magazine, <em>Eat Safe, Love</em>, to evaluate some of the ratings data in order to help their journalists and food critics decide where to focus future articles.</p>
  <h4>Part 1: Database and Jupyter Notebook Set Up</h4>
  <p>Use <code>NoSQL_setup_starter.ipynb</code> for this section of the challenge.</p>
  <ol>
    <li>
      <p>Import the data provided in the <code>establishments.json</code> file from your Terminal. Name the database <code>uk_food</code> and the collection <code>establishments</code>. Copy the text you used to import your data from your Terminal to a markdown cell in your notebook.</p>
    </li>
    <li>
      <p>Within your notebook, import the libraries you need: PyMongo and Pretty Print (<code>pprint</code>).</p>
    </li>
    <li>
      <p>Create an instance of the Mongo Client.</p>
    </li>
    <li>
      <p>Confirm that you created the database and loaded the data properly:</p>
      <ul>
        <li>List the databases you have in MongoDB. Confirm that <code>uk_food</code> is listed.</li>
        <li>List the collection(s) in the database to ensure that <code>establishments</code> is there.</li>
        <li>Find and display one document in the <code>establishments</code> collection using <code>find_one</code> and display with <code>pprint</code>.</li>
      </ul>
    </li>
    <li>
      <p>Assign the <code>establishments</code> collection to a variable to prepare the collection for use.</p>
    </li>
  </ol>
  <h4>Part 2: Update the Database</h4>
  <p>Use <code>NoSQL_setup_starter.ipynb</code> for this section of the challenge.</p>
  <p>The magazine editors have some requested modifications for the database before you can perform any queries or analysis for them. Make the following changes to the <code>establishments</code> collection:</p>
  <ol>
    <li>
      <p>An exciting new halal restaurant just opened in Greenwich, but hasn't been rated yet. The magazine has asked you to include it in your analysis. Add the following information to the database:</p>
      <pre><code>{
    "BusinessName":"Penang Flavours",
    "BusinessType":"Restaurant/Cafe/Canteen",
    "BusinessTypeID":"",
    "AddressLine1":"Penang Flavours",
    "AddressLine2":"146A Plumstead Rd",
    "AddressLine3":"London",
    "AddressLine4":"",
    "PostCode":"SE18 7DY",
    "Phone":"",
    "LocalAuthorityCode":"511",
    "LocalAuthorityName":"Greenwich",
    "LocalAuthorityWebSite":"http://www.royalgreenwich.gov.uk",
    "LocalAuthorityEmailAddress":"health@royalgreenwich.gov.uk",
    "scores":{
        "Hygiene":"",
        "Structural":"",
        "ConfidenceInManagement":""
    },
    "SchemeType":"FHRS",
    "geocode":{
        "longitude":"0.08384000",
        "latitude":"51.49014200"
    },
    "RightToReply":"",
    "Distance":4623.9723280747176,
    "NewRatingPending":True
}
</code></pre>
    </li>
    <li>
      <p>Find the BusinessTypeID for "Restaurant/Cafe/Canteen" and return only the <code>BusinessTypeID</code> and <code>BusinessType</code> fields.</p>
    </li>
    <li>
      <p>Update the new restaurant with the <code>BusinessTypeID</code> you found.</p>
    </li>
    <li>
      <p>The magazine is not interested in any establishments in Dover, so check how many documents contain the Dover Local Authority. Then, remove any establishments within the Dover Local Authority from the database, and check the number of documents to ensure they were deleted.</p>
    </li>
    <li>
      <p>Some of the number values are stored as strings, when they should be stored as numbers. Use <code>update_many</code> to convert <code>latitude</code> and <code>longitude</code> to decimal numbers.</p>
    </li>
  </ol>
  <h4>Part 3: Exploratory Analysis</h4>
  <p><em>Eat Safe, Love</em> has specific questions they want you to answer, which will help them find the locations they wish to visit and avoid.</p>
  <p>Use <code>NoSQL_analysis_starter.ipynb</code> for this section of the challenge.</p>
  <p>Some notes to be aware of while you are exploring the dataset:</p>
  <ul>
    <li>
      <p><code>RatingValue</code> refers to the overall rating decided by the Food Authority and ranges from 1-5. The higher the value, the better the rating. <strong>Note:</strong> This field also includes non-numeric values such as 'Pass', where 'Pass' means that the establishment passed their inspection but isn't given a number rating.</p>
    </li>
    <li>
      <p>The scores for Hygiene, Structural, and ConfidenceInManagement work in reverse. This means, the higher the value, the worse the establishment is in these areas.</p>
    </li>
  </ul>
  <p>Use the following questions to explore the database, and find the answers, so you can provide them to the magazine editors.</p>
  <p>Unless otherwise stated, for each question:</p>
  <ul>
    <li>
      <p>Use <code>count_documents</code> to display the number of documents contained in the result.</p>
    </li>
    <li>
      <p>Display the first document in the results using <code>pprint</code>.</p>
    </li>
    <li>
      <p>Convert the result to a Pandas DataFrame, print the number of rows in the DataFrame, and display the first 10 rows.</p>
    </li>
  </ul>
  <ol>
    <li>
      <p>Which establishments have a hygiene score equal to 20?</p>
    </li>
    <li>
      <p>Which establishments in London have a <code>RatingValue</code> greater than or equal to 4?</p>
      <p><strong>Hint:</strong> The London Local Authority has a longer name than "London" so you will need to use <code>$regex</code> as part of your search.</p>
    </li>
    <li>
      <p>What are the top 5 establishments with a <code>RatingValue</code> of '5', sorted by lowest hygiene score, nearest to the new restaurant added, "Penang Flavours"?</p>
      <p><strong>Hint:</strong> You will need to compare the geocode to find the nearest locations. Search within 0.01 degree on either side of the latitude and longitude.</p>
    </li>
    <li>
      <p>How many establishments in each Local Authority area have a hygiene score of 0? Sort the results from highest to lowest, and print out the top ten local authority areas.</p>
      <p><strong>Hint:</strong> You will need to use the <code>aggregation</code> method to answer this.</p>
      <p>The first 5 rows of your resulting DataFrame should look something like this:</p>
      <table>
        <thead>
          <tr>
            <th></th>
            <th>_id</th>
            <th>count</th>
          </tr>
        </thead>
        <tbody>
          <tr>
            <td>0</td>
            <td>Thanet</td>
            <td>1130</td>
          </tr>
          <tr>
            <td>1</td>
            <td>Greenwich</td>
            <td>882</td>
          </tr>
          <tr>
            <td>2</td>
            <td>Maidstone</td>
            <td>713</td>
          </tr>
          <tr>
            <td>3</td>
            <td>Newham</td>
            <td>711</td>
          </tr>
          <tr>
            <td>4</td>
            <td>Swale</td>
            <td>686</td>
          </tr>
        </tbody>
      </table>
    </li>
  </ol>
