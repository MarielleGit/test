## How to Import and Run:
1. Go to the repository on GitHub and **download the collection file**:  
   - 'OpenChargeMap API Tests - Station POIs & Reference Data.postman_collection.json'  
   - To download:  
     - Click on the file in GitHub.  
     - Press **Download raw file** or **Save link as...**.  

2. Open **Postman**.  
3. Click **Import** (top left).  
4. Select the JSON file you just downloaded.  
5. The collection will appear as:  
   **OpenChargeMap API Tests – Station POIs & Reference Data**.  

##  Setting up the API Key

The collection uses the variable '{{api_key}}' for authentication.

### How to obtain a key
- Visit [https://map.openchargemap.io/#/search](https://map.openchargemap.io/#/search).
- Open browser DevTools (**F12 → Network**).
- Inspect calls to 'api.openchargemap.io'.
- Copy the value of the query parameter 'x-api-key=...'.

## Configure authentication:  
   - Select the collection.  
   - Go to the **Auth** tab.  
   - Set:  
     - **Type**: 'Bearer Token'  
     - **Token**: paste your valid OpenChargeMap API key  

- Save the collection.  
## Running the Collection (Automated):
### Steps
1. In Postman, go to the **Collections** level.  
2. Hover over **OpenChargeMap API Tests – Station POIs & Reference Data**.  
3. Click the **...** (three dots) menu → select **Run**.  
4. The **Collection Runner** window will open.  
5. Make sure both requests are selected:  
   - '1) Get POIs (exactly 5 within 10km of London)'  
   - '2) Get Reference Data (ChargerTypes & StatusTypes)'  
6. Keep the default settings (Iterations = 1, Delay = 0).  
7. Click **Run OpenChargeMap API Tests – Station POIs & Reference Data**.
   
**Note:** On the **first run**, one or two tests may occasionally fail due to response caching or data variability. From the **second run onwards**, the results tend to stabilize and all tests pass consistently (except for known dataset mismatches, such as “Fast/Slow” wording differences).

## Test Results & Observations

Collection executed: **OpenChargeMap API Tests – Station POIs & Reference Data**

### 1) Get POIs
- ✅ Status code = 200
- ✅ Response time < 1000 ms
- ✅ Response is a valid JSON array
- ✅ Exactly 5 results returned
- ✅ Each POI has required fields ('ID', 'AddressInfo.Latitude', AddressInfo.Longitude', 'NumberOfPoints')
- **All tests passed (5/5)**

### 2) Get Reference Data
- ✅ Status code = 200
- ✅ Response time < 1000 ms
- ✅ Arrays 'ChargerTypes' and 'StatusTypes' present
- ✅ Items in both arrays have 'ID' and 'Title'
- ✅ StatusTypes have unique IDs
- ❌ **FAILED**: *ChargerTypes includes Fast and Slow*  
  - Assertion failed because the dataset did not explicitly contain the strings “Fast” and “Slow”.  
  - Likely reason: the API uses alternative labels (e.g., “Rapid” instead of “Fast”).

**Overall**: 11/12 tests passed successfully.

##  Assumptions & Limitations:
- Response times may occasionally exceed 1000ms depending on internet connection.
- The check for “Fast” and “Slow” assumes those exact English terms are present. If OpenChargeMap uses different terms (e.g., “Rapid”), the test will fail.

