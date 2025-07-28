# Task 4: Embeddings and Vector Database

???+ blank "Embeddings"

    ??? info "Introduction"

        === "Introduction"
            
            * Vector databases are specialized databases designed to store content like PDFs, blogs, Word documents, images, audio files, and videos as embedding vectors. This enables semantic-based retrieval, meaning the database can understand the meaning and context of the stored data, allowing for more accurate and relevant search results beyond simple keyword matching.

            ![vD](./assets/task4/v.png)

            * In the process of a large language model, embedding is generally the first step to convert discrete tokens (like words or subwords) into dense vector representations, which will allow the rest of the network to do the math necessary to predict the next word. Embeddings and vector databases are essential if you are building any kind of an AI product.

            ![EV](./assets/task4/ev.png)

            <p align="right"><a href="http://127.0.0.1:8000/Task4/#__tabbed_1_2" class="md-button md-button--primary">Next</a></p>

        === "What are embeddings?"

            Embeddings are basically data which are converted into an array of numbers called vectors that contain a pattern of relationships and can be used for similarity search. 

            ![Emb1](./assets/task4/emb1.png)


            ![Emb2](./assets/task4/emb2.png)

            Let's explain this concept using a 2D graph. In this graph, words like "Webex" and "collaboration" are often used in similar contexts, so their embeddings essentially vector representations are positioned close to each other (as shown in green in the below image ). These vectors are numerical arrays that computers can easily interpret.

            The advantage of using vectors is that we can find similar items by calculating the distances between their vectors, a process known as nearest neighbor search. However, simply storing these embeddings isn't enough. Performing queries across thousands of vectors can be incredibly slow. To overcome this, the vectors need to be indexed in the vector database. Indexing organizes the vectors in a way that speeds up the search process, allowing for quicker and more efficient retrieval of similar items.

            <span class="colour" style="color:red"> Note: In reality vectors can have hundred of dimensions </span>

            ![Emb3](./assets/task4/emb3.png)

            Similarly, images are also broken into vectors, which are arrays of numbers that machines can process. Once these embeddings (both for words and images) are generated, they are stored in a specialized database known as a vector database.

            ![Emb4](./assets/task4/emb4.png)

            There are numerous embedding models available, such as Google's Word2Vec, CLIP (Contrastive Language–Image Pretraining), and even those provided by OpenAI, which offer excellent capabilities for generating embeddings. However, the challenge is that these models don't include tools for storing and managing those embeddings. This is where vector databases become essential.

            !!! note
                In this lab session, we will be using OpenAI embeddings. More info can be found [here](https://platform.openai.com/docs/guides/embeddings)
            
            <p align="right"><a href="http://127.0.0.1:8000/Task4/#__tabbed_2_1" class="md-button md-button--primary">Next</a></p>

???+ blank "Vector Databases"

    ??? info "Introduction"

        === "Why use vector databases when we have relational databases?"
        
            Around 80% of the data we encounter is unstructured, including social media posts, images, and videos. This type of data doesn’t easily fit into traditional relational databases, which is where vector databases come into play.

            ![VecDB](./assets/task4/vdb.png)

            ![VecDB1](./assets/task4/ex_vdb.png)
        
        <p align="right"><a href="http://127.0.0.1:8000/Task4/#__tabbed_3_1" class="md-button md-button--primary">Next</a></p>

???+ blank "Understanding the workings of Embeddings and Vector Databases"

    ??? info "Introduction"

        === "Practical Example of Embedding Techniques Using Postman"
        
            ![SingleStore](./assets/task4/HLO.png)

            The above image illustrates a high-level overview of how embeddings and vector databases will work together:

            * Questions/Input Data: The process begins with a set of questions or inputs that need to be understood or processed.

            * Create Embeddings: These questions or inputs are then converted into embeddings.

            * Embeddings: Once the embeddings are generated, they are stored temporarily and prepared for the next step. These embeddings are essentially numeric representations that contain the contextual information of the original input.

            * Vector Database (Vector DB): The generated embeddings are stored in a vector database(e.g Singlestore). This database is optimized for searching and retrieving embeddings quickly, enabling faster queries when comparing vectors to find similar items.

            !!! note
                There are many vector databases, such as Chroma, Faiss, Pinecone e.t.c. However, we are using SingleStore for its ease of use and to help you better understand how embeddings are created.
            
            <p align="right"><a href="http://127.0.0.1:8000/Task4/#__tabbed_3_2" class="md-button md-button--primary">Next</a></p>

        === "LAB"
            === "Set OpenAI token"

                !!! important

                    If you’ve already obtained the token in previous steps/section, you can skip this section. It should be in the .txt file you downloaded at the beginning of the lab.
                
                * First, create an account from the <a href="https://platform.openai.com/" target="_blank">OpenAI official website</a>.

                * Create a new project API key by browsing to <a href="https://platform.openai.com/api-keys" target="_blank">API Keys web page</a>. Select Create new secret key. The API key is automatically generated. Save the APi Key as we will be using it in the later steps .

                ![GPT1_apiKey](./assets/task8c/ap.png)

                !!! note
                    We will use the OpenAI key in Postman to generate embeddings.
                
                <p align="right"><a href="http://127.0.0.1:8000/Task4/#__tabbed_4_2" class="md-button md-button--primary">Next</a></p>

            === "Login to Postman"

                If you haven't installed Postman on your machine yet, you can download it from the following <a href="https://www.postman.com/downloads/" target="_blank">link</a>

                !!! note
                    If you are using the provided machines, Postman will already be pre-installed.

                We will use embedding APIs to create an embedding vector that represents our input text. More information about OPENAI embeddings can be found at the following <a href="https://platform.openai.com/docs/api-reference/embeddings" target="_blank">link</a>

                The POST request we will be using:

                ``` https
                https://api.openai.com/v1/embeddings
                ```
                * Open Postman, create a new request by pressing +. Select POST as your request and enter the request url  

                ![postman1](./assets/task4/pm1.png)

                * Click on the Headers tab and enter the Following creds

                ```JSON
                Authorization: Bearer <replace with your openAi API key>
                Content-Type : application/json
                ```

                !!! note
                    Ensure there is a space between "Bearer" and your OpenAI API key.

                ![postman2](./assets/task4/pm2.png)

                In this lab, we will be using the [text-embedding-ada-002 model](https://platform.openai.com/docs/guides/embeddings/embedding-models), but feel free to use any other embedding model of your choice.

                ![Em2](./assets/task4/em1.png)

                !!! note
                    In the input field below, you can also enter your own text if you prefer.

                * In Postman, click on the "Body" tab, select **RAW** and enter the following information, and then press **Send**.

                ``` json
                {
                    "input": "What is WebexOne 2024? WebexOne is an annual in-person and virtual event that takes place over four days. It’s an event focused on AI collaboration and customer experience, and it features a range of activities such as insightful breakout sessions, technical training courses, hands-on labs, inspiring keynotes, epic entertainment, a solutions showcase and expo, customer awards, meet the experts, 1:1 executive meetings, a partner program, and more!",
                    "model": "text-embedding-ada-002"
                }
                ```

                ![postman3](./assets/task4/pm3.png)

                * You will receive a 200 OK message, confirming success. You'll notice that our text has been converted into embeddings (vectors/floating point numbers). In the upcoming steps, we will learn how to manually save this information in a vector database.

                ![postman4](./assets/task4/pm4.png)

                !!! note
                    Text embedding models convert text into numerical data (embeddings) that represent the meaning of the text.
                
                <p align="right"><a href="http://127.0.0.1:8000/Task4/#__tabbed_4_3" class="md-button md-button--primary">Next</a></p>

            === "Inserting values in Vector Database"
                
                We have a variety of databases available. In the upcoming step, let's demonstrate how to use <a href="https://www.singlestore.com/built-in-vector-database/" target="_blank">SingleStore</a> as a vector database and save our embeddings there.

                !!! note
                    This MANUAL step is simply to illustrate how embeddings are stored in vector databases.
                    
                    We will create a Free account on <a href="https://www.singlestore.com/built-in-vector-database/" target="_blank">SingleStore</a> since it provides some credits to set up a trial account.</span>

                !!! important
                    If you encounter an error while inserting data, try deleting the table and running the insert again.

                ![SS1](./assets/task4/st1.png)

                * I’m choosing to create an account using Google, but feel free to use any other method that works for you.

                ![SS2](./assets/task4/st2.png)

                * Select Continue

                ![SS3](./assets/task4/st3.png)

                ![SS31](./assets/task4/st31.png)

                ![SS4](./assets/task4/st4.png)

                ![SS4a](./assets/task4/st4a.png)

                ![SS4b](./assets/task4/st4b.png)

                ![SS5](./assets/task4/st5.png)

                * Click on Create New -> Deployment

                ![SS6](./assets/task4/st6.png)

                * Give your workspace a name, keep all other settings at their default, and click "Next."

                ![SS7](./assets/task4/st7.png)

                * Then, leave everything as is and click on "Create Workspace."

                ![SS8](./assets/task4/st8.png)

                !!! note
                    Workspace creation can take up to 5 minutes.

                * Now we can create a database

                ![SS9](./assets/task4/st9.png)
                
                !!! note
                    Database creation can take up to 5 minutes.

                ![SS11](./assets/task4/st11.png)

                * Click on Database tab and click on the databse name you created earlier.

                ![SS13](./assets/task4/st13.png)

                * Navigate to Develop > Data Studio. Open the SQL Editor.

                ![SS14](./assets/task4/st14.png)

                *  Be sure to select your workspace and database.

                ![SS15](./assets/task4/st15.png)

                * Run this SQL command to create a table called myvectortable  - Press Run

                !!! note
                    You can also name the table as you prefer. 
                    Please note: If your lab remains inactive for 20 minutes, the SingleStore database will automatically pause. To resume, go back to the homepage, click 'Resume,' and your workspace will be ready again within a few minutes."

                ```sql
                create table if not exists myvectortable (
                text TEXT,
                vector BLOB
                );
                ```
                ![SS16](./assets/task4/st16.png)

                * You can navigate to the Schema Explorer VIEW on the right, and verify that the table has been created.

                ![SS171](./assets/task4/st171.png)

                !!! important
                    OR

                * Navigate to the Deployments tab, click on Databases, select your database, and verify that the table has been created.

                ![SS17](./assets/task4/st17.png)

                !!! note
                    The table name we created earlier may differ from the one shown in the image above. In our case, we named the table myvectortable.

                * Let's copy the embeddings we generated earlier using Postman so that we can insert them into our database.

                * To proceed, copy the input text (from the input field only) and all the values from the 'embedding' field (in reponse), including the square brackets [ ], as shown in the image. These will be used for insertion into our database.

                ![SS18](./assets/task4/st18.png)

                * Let's head back to our SQL editor and insert the values into our database using the below SQL command. Once done press "Run"

                !!! important
                    You can reuse the same SQL editor block, remove the previous command, and run the following one.

                ```sql
                insert into myvectortable (text ,vector) values ("your_input_text", JSON_ARRAY_PACK("your_embeddings"))
                ```

                !!! note
                    In this query:
                    
                    - <b style="color: red;">Replace "your_input_text" with the input values from Postman.</b>
                    - <b style="color: red;">Replace "your_embeddings" with the embeddings you copied earlier, including the square brackets [ ].</b>



                ``` sql
                insert into myvectortable (text ,vector) values ("What is WebexOne 2024? WebexOne is an annual in-person and virtual event that takes place over four days. It’s an event focused on AI collaboration and customer experience, and it features a range of activities such as insightful breakout sessions, technical training courses, hands-on labs, inspiring keynotes, epic entertainment, a solutions showcase and expo, customer awards, meet the experts, 1:1 executive meetings, a partner program, and more!", JSON_ARRAY_PACK("[
                                -0.0042485874,
                                -0.02296605,
                                0.011213377,
                                0.01114761,
                                -0.027280405,
                                0.0023528363,
                                -0.004350527,
                                0.0043768343,
                                -0.00068562734,
                                -0.011660597,
                                0.010397859,
                                0.018730614,
                                -0.0158763,
                                -0.013469206,
                                0.0026997605,
                                -0.00003768792,
                                0.014850326,
                                -0.03183152,
                                0.0026175508,
                                -0.0459321,
                                -0.0055803815,
                                -0.008247258,
                                -0.011713211,
                                0.0006169824,
                                -0.017112732,
                                -0.002885554,
                                -0.004113764,
                                -0.01348236,
                                ........
                            ]"))
                ```

                * After running the above command, you will see that our table now contains both the input text and the corresponding embeddings. Click on Sample Data

                ![SS19](./assets/task4/st19.png)

                * Let's now explore on how to retrive values from Vector Database

                <p align="right"><a href="http://127.0.0.1:8000/Task4/#__tabbed_4_4" class="md-button md-button--primary">Next</a></p>


            === "Retrieving Values from the Vector Database"

                ![SS20](./assets/task4/st20.png)

                * Searching the vector database is quite simple. Example: we want to find information related to WebexOne. To do this, we'll create embeddings for our query, "Is WebexOne an annual event?" and then search the vector database to find matches against the existing embeddings.

                ```py linenums="1"
                Is WebexOne an annual event?
                ```

                * Let's open Postman and create an embedding for our question now. Be sure to click on "Send."

                !!! note
                    Make sure you use the same embedding techniques that we used earlier.

                ![SS21](./assets/task4/st21.png)

                * Let's head over to the SQL editor and run a query for our search.

                ![SS2111](./assets/task4/st2111.png)

                !!! note
                    You can reuse the same SQL editor block, remove the previous command, and run the following one.

                ``` sql
                select text,dot_product(vector,JSON_ARRAY_PACK("your_embeddings")) as score
                from myvectortable
                order by score desc
                limit 5;
                ```

                !!! note
                
                    In this query:

                    - <b style="color: red;">Replace "your_embeddings" with the embeddings you copied earlier, including the square brackets [ ].</b>

                    <span class="colour" style="color:red">Note: The below code is just an example, please copy the embeddings from your Postman. </span>

                ```sql 
                select text,dot_product(vector,JSON_ARRAY_PACK("[
                                -0.0015118581,
                                -0.021267666,
                                0.023597047,
                                -0.0072638104,
                                -0.02286653,
                                0.005909599,
                                -0.026119394,
                                -0.010268575,
                                0.0052169873,
                                -0.009551842,
                                0.024065679,
                                0.020178782,
                                0.015464887,
                                0.016815653,
                                -0.016333235,
                                -0.0006641838,
                                0.018069934,
                                -0.010564916,
                                0.007911626,
                                -0.026367495,
                                -0.0019417254,
                                -0.005547787,
                                -0.012604848,
                                0.0003715036,
                                -0.013962504,
                                0.011729606,
                                -0.00078737224,
                                -0.011881223,
                                0.007815143,
                                0.009992908,
                                0.020316616,
                                -0.0032580325,
                                -0.0066401153,
                                0.0097310245,
                                -0.0028652078,
                                -0.008145943,
                                -0.0074843434,
                                ........
                            ]")) as score
                from myvectortable
                order by score desc
                limit 5;

                ```

                ![SS22](./assets/task4/st22.png)

                <span class="colour" style="color:red">Note: You’ll be able to see the success of the vector database—higher scores indicate better matches for the answer.</span>

                <p align="right"><a href="http://127.0.0.1:8000/Task4/#__tabbed_4_5" class="md-button md-button--primary">Next</a></p>

            === "Conclusion"
            
                In summary, vector databases allow LLMs to have long-term memory. In this section, we explored how to use embeddings and vector databases by generating embeddings with the OpenAI API through Postman. After setting up a free SingleStore account, embeddings were stored in a vector database. The process included creating an embedding for a query, searching the database, and confirming that it effectively retrieved relevant information. This demonstrated how vector databases can efficiently manage and query embeddings, making it easier to find relevant information based on the data stored.
            
                <p align="right"> 👉 This concludes the task. Click the <strong>"Context Windows and Retrieval Augmented Generation (RAG) "</strong> Task on the left. </p>