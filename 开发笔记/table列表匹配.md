```js
          <el-table-column

            prop="rcCreatePerson"

            align="center"

            label="创建人"

            :formatter="rcCreatePersonFormatter"

            show-overflow-tooltip

          ></el-table-column>

    // 创建人

    rcCreatePersonFormatter(row, column, cellValue) {

      try {

        return this.userList.find((item) => item.userId === cellValue).userName;

      } catch (e) {

        return cellValue;

      }

    },
```