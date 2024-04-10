# 🛰️ Axios

Details about different wasy to fetch api using axios.


## 👨‍💻 Authors

- [@vijayaselvam](https://www.github.com/vijayaselvam)


## 🏷️ Topics

- [x]  Axios Asynchronous Call
- [x]  AXIOS - Passing headers
- [x]  Passing Headers in Request
- [x]  Axios base url - Default Configurations
- [x]  Create Instance and Call API
- [x]  Axios using Interceptors.




## 01. Axios Asynchronous Call

✔️ Using Aync to fetch api

```
  const fetchData = async () => {
        const response = await axios.get(
          `http://localhost:8888/api/Employee/GetAllEmployees`
        );
```

## Implementation
```Async
  useEffect(() => {
    const fetchData = async () => {
      try {
        const response = await axios.get(
          `http://localhost:8888/api/Employee/GetAllEmployees`
        );
        if (response.status === 200) {
          console.log(response.data);
        }
      } catch (error) {
        console.log(error);
      }
    };
    fetchData();
  }, []);
```

## 02. AXIOS - Passing headers

✔️ Pass HTTP Method and URL and required details as a parameter

```
const response = await axios({ 
  method : "get",
  url : "http://localhost:8888/api/Employee/GetAllEmployees"
});
```

### Implementation
```
  useEffect(() => {
    const fetchData = async () => {
      try {
        const response = await axios({ method : "get",
         url : "http://localhost:8888/api/Employee/GetAllEmployees"
      });
        if (response.status === 200) {
          console.log(response.data);
        }
      } catch (error) {
        console.log(error);
      }
    };
    fetchData();
  }, []);
```


## 03. Passing Headers in Request

✔️  Passing Headers into request as below
```
 const token = 'Test'
 const response = await axios.get(
          `http://localhost:8888/api/Employee/GetAllEmployees`,{
            headers:{
              Authorization: `Bearer ${token}`
            }
          }
        );
```

### Implementation
```
  const token = 'Test'
  useEffect(() => {
    const fetchData = async () => {
      try {
        const response = await axios.get(
          `http://localhost:8888/api/Employee/GetAllEmployees`,{
            headers:{
              Authorization: `Bearer ${token}`
            }
          }
        );
        if (response.status === 200) {
          setAPIData(response.data);
          setLoading(true);
        } else {
          setLoading(false);
        }
      } catch (error) {
        console.log(error);
      }
    };
    fetchData();
  }, []);
```

## 04. Axios base url - Default Configurations
  ✔️  This will set up axios baseurl in the app.js and we can use it with in applications  
  ✔️  No need to create an Instance.

  ✔️  Not only base url we can set baseurl, Timeout and other all configs.

⚙️ Create Base URL as below

```axios.defaults.baseURL = 'http://localhost:8888/api/Employee'```

### Implementation
  ```React Base URL
  axios.defaults.baseURL = 'http://localhost:8888/api/Employee'
  useEffect(() => {
    const fetchData = async () => {
      try {
        const response = await axios.get(
          `/GetAllEmployees`
        );
        if (response.status === 200) {
          console.log(response.data);
        } 
      } catch (error) {
        console.log(error);
      }
    };
    fetchData();
  }, []);
```

## 05. Create Instance and Call API

✔️  Create common Axios instance and use to fetch api's

```React
import  axios  from "axios";

export const instance = axios.create({
    baseURL: 'http://localhost:8888/api/Employee',
    timeout : 5000,
});
```

## Instance Creation

✔️ Import axios from axios package

```
import  axios  from "axios";
```

✔️  Using Create to create the instance and map your endpoint baseURL

✔️  Timeout seconds we can add here.

✔️  Instance created in one place and utilized in all over application

```
export const instance = axios.create({
    baseURL: 'http://localhost:8888/api/Employee',
    timeout : 5000,
});
```

## Implementation

✔️ `instance` - Axios instance

✔️  `get` is api method to get all employees details.(Ex Get, POST, PUT, DELETE etc...)

✔️ once api response is received checking the request is success by `Status is 200`

✔️  Put `Try catch` to catch Network errors and other errors

```
const fetchData = async () => {
    try {
      const response = await instance.get(
        `/GetAllEmployees`
      );
      if (response.status === 200) {
        console.log(response.data);
      } 
    } catch (error) {
      console.log(error);
    }
  };
```



## 06. Axios using Interceptors.
  ✔️  Interceptors used to config before request and after response

  ```
  axios.defaults.baseURL = 'http://localhost:8888/api/Employee'
  ```

  ✔️  Modifying request `Authorization` key in runtime(dynamic)

```
  axios.interceptors.request.use((config) => {
    console.log(config);
    return{...config,headers:{...config.headers, Authorization: "Bearer Token"}}
  }, (error) => console.log(error)); 
```

  ### Modifying request Without any config data

```
  axios.interceptors.request.use((config) => {
    console.log(config);
    return config
  }, (error) => console.log(error)); 
```
 ✔️  Modifying response from service call
 ```
 axios.interceptors.response.use((response) => {
  //Taking response into data and adding title in response
  return {...response, data:{ resp: response.data, title : "apiResponse"}}
  console.log(response);
}, (error) => console.log(error));  
```
