# Cloud Firestore

🔗 *<u>[Notes for Firebase](../README.md)</u>/<u>[Firestore](#)</u>*

## ■ Initialization
```js
firebase.initializeApp({
  apiKey: 'FIREBASE_API_KEY',
  authDomain: 'FIREBASE_AUTH_DOMAIN',
  projectId: 'CLOUD_FIRESTORE_PROJECT_ID',
});

var db = firebase.firestore();
```
&nbsp;
## ■ Data structure
```
ROOT ________ Collections A
    |________ Collections B
              |______________ Document ID 1
              |               |____________ Field 1
              |               |____________ Field 2
              |               |____________ ...
              |
              |______________ Document ID 2
```
&nbsp;
## ■ Refer a collection
```js
db.collection(COLLECTION_NAME); // collectionRefer
```
&nbsp;
## ■ Refer a document
```js
db.collection(COLLECTION_NAME).doc(UNIQUE_DOCUMENT_ID); // documentRefer
```
&nbsp;
## ■ General syntax for CRUD

>> ```js
>> refer.[ACTION_CALL]
>>   .then(doc => /* action with doc */ )
>>   .catch(error => /* action with error */);
>> ```

**Notes:**

  | Key             | Value |
  | :---            | :----:   |
  | `refer`         | `collectionRefer`, `documentRefer`|
  | `[ACTION_CALL]` | `add()`, `set()`, `get()`, `delete()`, etc.|

*Get some specific cases in the bellow:*

&nbsp;

## ■ Add a document
```js
// Auto ID
collectionRefer.add({
  [KEY]: [VALUE],
});

// Custom ID
collectionRefer.doc(UNIQUE_DOCUMENT_ID).set({
  [KEY]: [VALUE],
});
```


**Notes:**
*`Documents` in a `collection` can contain `different-sets-of-information`(`key-value pair`).*

&nbsp;
## ■ Update a document
```js
documentRefer.update({
  [KEY]: [VALUE],
});
```
&nbsp;
## ■ Delete a document
```js
collectionRefer.doc(UNIQUE_DOCUMENT_ID).delete();
```
&nbsp;
## ■ Get all documents
```js
collectionRefer.[OPTION_CALL].get()
  .then((snapshot) => {
    snapshot.forEach((doc) => {
      console.log(`${doc.id} => ${doc.data()}`);
    });
  }
);
```

| Key             | Value |
| :---            | :----:   |
| `[OPTION_CALL]` | `null`, `orderBy()`, `where()`, `startAt()` etc. |

**Notes:**
*`[OPTION_CALL]` supports **`Method chaining`**:*

```js
collectionRefer.[ACTION_CALL_1].[ACTION_CALL_2]...[ACTION_CALL_N].get()
```

*Get some specific cases in the bellow:*

&nbsp;
### ■ Get all documents by condition

```js
collectionRefer.where('population', '>', 100000)
```
&nbsp;
### ■ Get all documents by order
```js
collectionRefer.orderBy(FIELD_NAME, ORDER_TYPE);
```
| Key             | Value |
| :---            | :----:   |
| `FIELD_NAME`         | `FIELD_NAME`|
| `ORDER_TYPE`         | `null`, `asc`*(default)*, `desc`|

**Notes:**
- *If you include a filter with a range comparison `(<, <=, >, >=)`, your first ordering must be on the same field. For example:*
  ```js
  collectionRefer.where('count', '>', 100000).orderBy('count', 'desc'); // Correct
  collectionRefer.where('count', '>', 100000).orderBy('name');          // Incorrect
  ```

- *`orderBy()` filters for existence-of-the-given-fields (not include documents not containing the given fields).*

&nbsp;
### ■ Get all documents by limit
```js
collectionRefer.limit(COUNT);
```
| Key             | Value |
| :---            | :----:   |
| `COUNT`         | *number type*|
