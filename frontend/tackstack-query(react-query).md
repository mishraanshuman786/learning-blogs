# React Query: Simplifying Date Fetching and Caching

# What is react Query?
It is a library for fetching data in a React Component.

# Why?
1. Since React is a UI library, there is no specific pattern for data fetching.
2. We typically use the useEffect hook for data fetching and useState hook to maintain component state like loading, error state or the resulting data.
3. If the data is needed throughout the app, then we tend to use state management libraries like redux.
4. Most of the state management libraries are good for working with client state. Ex. 'theme' for an application / whether a modal is open.
5. State Management Libraries are not great for working with asynchronous or server state.

# Client vs server state
Client state:
- Persisted in your app memory and accessing or updating it is synchronous.

Server state:
- Persisted remotely and requires asynchronous APIs for fetching or updating
- Has shared ownership
- Data can be updated by someone else without your knowledge.
- UI data may not be in sync with the remote sevrer/database data.
- Challenging when you have to deal with caching, deduplication of multiple requests for the same data, updating stale data in the background, performance optimizations in pagination and lazy-loading, etc. 

# Project Setup
1. New React Project setup using CRA
2. Setup an API Endpoint that serves mock data for use in our application
3. Setup react router and a few routes in the application
4. Fetch data the traditional way using useEffect and useState

## Setting up a new react app with the dependencies installed:

### 1. Run the command to create a new React App:
```
npx create-react-app react-query-demo
```

### 2. Setup an API endpoint that serves mock data for use in our application
For doing that we can use a very lightweight package we can call it as `json-server ` npm package.

For installing `json-server` package, run the following command:
```
npm install json-server
```

Then come to parent directory and create a file named `db.json` for storing the json data which we want to serve using json-server:
```
{
    "posts":[
        {
            "id":"1",
            "title":"Sunder Pichai Interview",
            "body":"Discussing The Future Of Tech"
        },
        {
            "id":"2",
            "title":"Marques Reviews Tesla",
            "body":"Tesla's latest EV Review"
        },
        {
            "id":"3",
            "title":"AI in 2024",
            "body":"Impact on daily Life"
        }
    ]
}
```

Add script in package.json file to startup the json-server:
```
"serve-json":"json-server --watch db.json --port 4000"
```

Then run on the terminal this command:
```
npm run serve-json
```

Now the server is started at this endpoint:
```
http://localhost:4000/posts
```

### 3. Now create a component to show the fetched data and create a file to hold the logic for fetching the data:
Install the axios library for fetching the data from json-server:
```
npm i axios
```

create a component to write the code for fetching the posts using Traditional Way (useEffect way):
Create a file named `PostsTraditional.tsx`:
```
import { useEffect,useState } from "react";

import axios from "axios";

const PostsTraditional = () => {

    const [posts,setPosts]=useState([]);
    const [isLoading,setIsLoading]=useState(true);
    const [isError,setIsError]=useState(false);

    const fetchPosts=async ()=>{
        try{
          const response=await axios.get("http://localhost:4000/posts");
          setPosts(response.data);
        }
        catch(error){
            setIsError(true);
        }
        finally{
            setIsLoading(false);
        }
    }

    useEffect(()=>{
       fetchPosts();
    },[]);

    if(isLoading) {
        return <div>Page is Loading...</div>
    }

    if(isError){
        return <div>Error has occurred...</div>
    }

  return (
    <div>
        <h2>Traditional Fetching</h2>
        {
            posts && (
                posts.map((post)=>{
                    return (
                      <div>
                        <h3>{post.id}</h3>
                        <h3>{post.title}</h3>
                        </div>
                    )
                })
            )
        }
    </div>
  )
}

export default PostsTraditional
```


