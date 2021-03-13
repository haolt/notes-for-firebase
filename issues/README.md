# Issues

🔗 *<u>[Notes for Firebase](../README.md)</u>/<u>[Issues](#)</u>*

*Current issues in AFL.*

## ■ Outline:

🔗 &nbsp; **Document list screen**.

🔗 &nbsp; **Document detail screen**.

&nbsp;

## ■ Document list screen.

&nbsp;

🔗&nbsp; **Task:** Màn list hiển thị danh sách theo `keywords` & `page`.

&nbsp;

🔗&nbsp; **Target:**

- Không fetch nhiều lần.
- Giảm lượng đọc.
- Sau khi xoá, cập nhật thì màn list cần được cập nhật lại (mà không cần fetch lại cả list).

&nbsp;

🔗&nbsp; **<u>Solution</u>:**

- [ ] Khi tạo document:

  ```js
  set updated_at = created_at = getServerTimeStamp(); // Type: Firebase timestamp
  set timestamp = firstDocumentInList.updated_at; // Type: Firebase timestamp
  ```

- [ ] Khi sửa document:

  ```js
  set updated_at = getServerTimeStamp(), // Type: Firebase timestamp
  set timestamp = firstDocumentInList.updated_at;
  ```

- [ ] Khi xoá document:

  ```js
  set updated_at = deleted_at = getServerTimeStamp(),
  set dataList = removeDocumentExceptDeletedId()
  ```

- [ ] **Vào màn list lần đầu**:

```js
collectionRef.orderBy("updated_at", "desc").get();
```

ta được `dataList`.

- [ ] **Vào màn list lần 1++** _(VD như lúc chuyển route hoặc vừa từ trang tạo, sửa hay confirm xoá về)_:

```js
collectionRef.where("updated_at" > timestamp).orderBy("updated_at");
```

ta được `updatedDataList` = `document (vừa tạo || vừa sửa || vừa xoá )`.

- [ ] Cập nhật `dataList` dựa vào `updatedDataList`:

- _Nếu document vừa được thêm thì đưa vào `dataList`._

- \*_Nếu document vừa được sửa thì cũng đưa vào `dataList`, đồng thời xoá chính nó trong `dataList cũ` dựa vào `id`._

  ```js
  _.uniqBy(companies.concat(state.companies), "id");
  ```

- _Nếu document vừa được xoá thì được lọc thông qua `deleted_at`_.

&nbsp;

## ■ Document detail screen

🔗&nbsp; **Task:**

- Màn detail hiển thị chi tiết document.

&nbsp;

🔗&nbsp; **Target:**

- Chỉ hiển thị document có `id` tương ứng và `chưa-bị-xoá`.

&nbsp;

🔗&nbsp; **Solution:**

- Lấy document có `id` tương ứng về, client kiểm tra trường `deleted_at`.
