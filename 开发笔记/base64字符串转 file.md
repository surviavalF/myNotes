```js
      // base64字符串

      const base64String = "your_base64_string_here";

      // 将base64字符串转换为Blob

      const byteCharacters = atob(base64String);

      const byteNumbers = new Array(byteCharacters.length);

      for (let i = 0; i < byteCharacters.length; i++) {

        byteNumbers[i] = byteCharacters.charCodeAt(i);

      }

      const byteArray = new Uint8Array(byteNumbers);

      const blob = new Blob([byteArray], { type: "application/octet-stream" }); // Blob转为File对象

      const file = new File([blob], "filename.jpg", { type: 'image/jpeg' });
```