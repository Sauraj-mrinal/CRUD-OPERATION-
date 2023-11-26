# CRUD-OPERATION-

Step 1: The first two lines of the code initialize two variables:

app: This variable is assigned a reference to a Google Spreadsheet specified by its URL.
sheet: This variable is assigned a reference to a specific sheet within the spreadsheet specified by its name.
Step 2: The function doPost(e) is executed when a POST request is made to the URL of the script. This function performs the following steps:

The request data is parsed as a JSON object and assigned to a variable called obj.
The base64-encoded image data is decoded and assigned to a variable called dcode.
A new blob is created from the decoded data, with the specified MIME type and filename, and assigned to a variable called blob.
A new file is created in the user's Google Drive from the blob data and assigned to a variable called newFile.
The sharing permissions of the new file are set to "anyone with the link can view", and a URL for downloading the file is obtained and assigned to a variable called link.
The index of the last row in the sheet is obtained and assigned to a variable called lr.
A formula is set in the first column of the next row after the last row, which displays the image using the specified URL, and assigned to a range.
A plain text response indicating that the image was uploaded is returned.
If there was an error during the upload process, an error message is returned as a plain text response.

Html JavaScript Code
This is an HTML5 document that includes an input element of type "file" and an image element. It also includes a script that allows the user to select an image and sends it to an API endpoint URL using a POST request.

The script begins by declaring a variable called "url" and assigning it the value of "Api_Endpoint_Url". It then declares a variable called "file" and assigns it the value of the first input element on the page. The script also declares a variable called "img" and assigns it the value of the first image element on the page.

The script adds an event listener to the "change" event of the "file" input element. When the user selects a file, the script creates a new FileReader object called "fr" and adds an event listener to the "loadend" event of the FileReader object. When the FileReader object has finished loading the selected file, the script sets the "src" attribute of the "img" element to the result of the FileReader object.

The script then splits the "res" variable into an array, using the string "base64," as the separator, and assigns the second element to a variable called "spt". It creates an object called "obj" with three properties: "base64", "type", and "name". The "base64" property is set to the value of "spt", the "type" property is set to the MIME type of the selected file, and the "name" property is set to the name of the selected file.

The script then sends a POST request to the URL specified in the "url" variable, with the "obj" object as the request body. It waits for the response from the server and converts it to text. Finally, it logs the response data to the console.

<!-- This is the doctype declaration for an HTML5 document -->
<!DOCTYPE html>
<!-- This is the opening HTML tag, and the "lang" attribute specifies the language of the document -->
<html lang="en">
<head>
    <!-- This meta tag sets the character set to UTF-8 -->
    <meta charset="UTF-8">
    <!-- This meta tag tells IE to use the latest rendering engine -->
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <!-- This meta tag sets the viewport to the width of the device and sets the initial zoom level to 1 -->
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <!-- This sets the title of the webpage -->
    <title>Document</title>
</head>
<body>
<!-- This is an input element of type file, which allows the user to select an image -->
<input type="file"accept="image/*">
<!-- This is an image element with an empty src and alt attribute -->
<img src="" alt="">
<!-- This is a script tag, which contains JavaScript code -->
<script>
    // This line declares a variable called "url" and assigns it a value of "Api_Endpoint_Url"
    let url = "Api_Endpoint_Url";
    // This line declares a variable called "file" and assigns it the value of the first input element on the page
    let file = document.querySelector("input");
    // This line declares a variable called "img" and assigns it the value of the first image element on the page
    let img = document.querySelector("img");
    // This line adds an event listener to the "change" event of the "file" input element
    file.addEventListener('change',()=>{
        // This line creates a new FileReader object called "fr"
        let fr = new FileReader();
        // This line adds an event listener to the "loadend" event of the FileReader object
        fr.addEventListener('loadend',()=>{
            // This line declares a variable called "res" and assigns it the result of the FileReader object
            let res = fr.result;
            // This line sets the "src" attribute of the "img" element to the value of "res"
            img.src=res;
            // This line splits the "res" variable into an array, using the string "base64," as the separator, and assigns the second element to a variable called "spt"
            let spt = res.split("base64,")[1];
            // This line creates an object called "obj" with three properties: "base64", "type", and "name"
            let obj = {
                base64:spt,
                type:file.files[0].type,
                name:file.files[0].name
            }
            // This line sends a POST request to the URL specified in the "url" variable, with the "obj" object as the request body
            fetch(url,{
                method:"POST",
                body:JSON.stringify(obj)
            })
            // This line waits for the response from the server and converts it to text
            .then(r=>r.text())
            // This line logs the response data to the console
            .then(data=>console.log(data))
 
        })
        // This line reads the selected file as a data URL
        fr.readAsDataURL(file.files[0])
    })
</script>
</body>
</html>
