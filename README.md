# nosql-challenge



## Eat Safe, Love

1. **Database Setup:** The `NoSQL_setup.ipynb` notebook is used to set up and update the database.
2. **Data Analysis:** The `NoSQL_analysis.ipynb` notebook handles querying relevant information for analyses and converts the results into Pandas DataFrames.
3. **Data Import:** Data from the `establishments.json` file is imported using the following command in the Terminal: `mongoimport --type json -d uk_food -c establishments --drop --jsonArray establishments.json`. This command imports the data into the MongoDB database named 'uk_food', specifically into the 'establishments' collection, replacing any existing data in the collection.


------------------------------------------------------------------------------------------------------------------------------------------------------------------------------




**Set Up and Update Database**

This section involved several key operations on the database:

1. **Insert New Restaurant:** A new halal restaurant located in Greenwich was added to the database using the command:
   ```python
   establishments.insert_one(new_restaurant_data)
   ```

2. **Update Restaurant Details:** The business type ID for the newly added restaurant, 'Penang Flavours', was corrected using the command:
   ```python
   establishments.update_one({'BusinessName':'Penang Flavours'}, [{'$set':{'BusinessTypeID':1}}])
   ```

3. **Remove Specific Entries:** All entries for establishments located in Dover were removed from the database with:
   ```python
   establishments.delete_many({'LocalAuthorityName': 'Dover'})
   ```

4. **Convert Geocode to Decimal:** To facilitate analysis, latitude and longitude data were converted to decimal numbers:
   ```python
   establishments.update_many({}, [{'$set': {"geocode.latitude": {'$toDecimal': '$geocode.latitude'}}}])
   establishments.update_many({}, [{'$set': {"geocode.longitude": {'$toDecimal': '$geocode.longitude'}}}])
   ```

These operations ensure the database is properly configured and updated, paving the way for accurate and efficient data analysis in subsequent sections.


------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
                           


**Exploratory Analysis**

This section delves into various queries to uncover insights within the uk_food dataset:

1. **Hygiene Score Analysis:**
   - **Query:** Which establishments have a hygiene score equal to 20?
   - **Result:** There are 41 establishments with a hygiene score of 20.

2. **Rating Analysis in London:**
   - **Query:** Which establishments in London have a RatingValue greater than or equal to 4?
   - **Result:** There are 34 establishments in London with a RatingValue of 4 or higher.

3. **Top Establishments Near a New Restaurant:**
   - **Query:** What are the top 5 establishments with a RatingValue of '5', sorted by the lowest hygiene score, nearest to the new restaurant "Penang Flavours"?
   - **Result:** The top 5 are: "Volunteer", "Plumstead Manor Nursery", "Atlantic Fish Bar", "Iceland", and "Howe and Co Fish and Chips - Van 17".

4. **Hygiene Score Distribution by Local Authority:**
   - **Query:** How many establishments in each Local Authority area have a hygiene score of 0?
   - **Result:** There are notable entries from various authorities with the preview of the first 10 rows showing authorities like Thanet, Greenwich, and Maidstone among others, indicating the distribution of establishments with the lowest hygiene score.



----------------------------------------------------------------------------------------------------------------------------------------------------------------------------- 



#### Resources

For the successful execution of this project, the following resources were utilized:

- **Class Lectures, Notes, and Activities:** These provided foundational knowledge and practical skills necessary for undertaking the project tasks.
- **Xpert Learning Assistant:** This tool was invaluable for troubleshooting code issues and offering explanations on why certain methods are more efficient than others.
- **establishments.json:** This file served as the primary data source, containing detailed information about various establishments that was essential for our analyses.

These resources collectively supported the project’s objectives, ensuring a thorough approach to data analysis and problem-solving.
