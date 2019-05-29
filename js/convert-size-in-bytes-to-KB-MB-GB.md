# Function
```JS
function formatBytes(bytes,decimalPoint) {
    if(bytes == 0) return '0 Bytes';
    var k = 1000,
       dm = decimalPoint || 2,
       sizes = ['Bytes', 'KB', 'MB', 'GB', 'TB', 'PB', 'EB', 'ZB', 'YB'],
       i = Math.floor(Math.log(bytes) / Math.log(k));
    return parseFloat((bytes / Math.pow(k, i)).toFixed(dm)) + ' ' + sizes[i];
}
```
# Usage :
```JS
// formatBytes(bytes,decimals)

formatBytes(1024);       // 1 KB
formatBytes('1024');     // 1 KB
formatBytes(1234);       // 1.21 KB
formatBytes(1234, 3);    // 1.205 KB
```
# References 
https://stackoverflow.com/questions/15900485/correct-way-to-convert-size-in-bytes-to-kb-mb-gb-in-javascript
https://www.codexworld.com/how-to/convert-file-size-bytes-kb-mb-gb-javascript/
