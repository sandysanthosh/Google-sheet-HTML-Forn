# Google-sheet-HTML-form

https://hayykel.blogspot.com/2021/08/how-to-create-form-with-google-apps.html


#### Code.gs:

```
function doGet(request) {
  return HtmlService.createTemplateFromFile('Index').evaluate();
  
}

function include(filename){
  return HtmlService.createHtmlOutputFromFile(filename).getContent();
}

function processForm(formObject){
  var url="";
  var ss= SpreadsheetApp.openByUrl(url);
  var ws=ss.getSheetByName("Data");

  ws.appendRow([
    formObject.first_name,
    formObject.last_name,
    formObject.gender,
    formObject.dateOfBirth,
    formObject.email,
    formObject.phone

  ]);
}

```

#### index.html 

```


Index.html
<!DOCTYPE html>
<html>
  <head>
  
    <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/bootstrap@4.5.3/dist/css/bootstrap.min.css"
 integrity="sha384-TX8t27EcRE3e/ihU7zmQxVncDAy5uIKz4rEkgIXeMed4M0jlfIDPvg6uqKI2xXr2" 
crossorigin="anonymous">
  <?!= include('JavaScript'); ?>
  </head>
  
  <body>
    <div class="container">
            <div class="row">
                <div class="col-6">
                    <form id="myForm" onsubmit="handleFormSubmit(this)">
                        <p class="h4 mb-4 text-center">Contact Details</p>

                        <div class="form-row">
                            <div class="form-group col-md-6">
                                <label for="first_name">First Name</label>
                                <input type="text" class="form-control" id="first_name" name="first_name" placeholder="First Name">
                            </div>
                            <div class="form-group col-md-6">
                                <label for="last_name">Last Name</label>
                                <input type="text" class="form-control" id="last_name" name="last_name" placeholder="Last Name">
                            </div>
                        </div>

                        <div class="form-row">
                            <div class="form-group col-md-6">
                                <p>Gender</p>
                                <div class="form-check form-check-inline">
                                    <input class="form-check-input" type="radio" name="gender" id="male" value="male">
                                    <label class="form-check-label" for="male">Male</label>
                                </div>
                                <div class="form-check form-check-inline">
                                    <input class="form-check-input" type="radio" name="gender" id="female" value="female">
                                    <label class="form-check-label" for="female">Female</label>
                                </div>
                            </div>
                            <div class="form-group col-md-6">
                                <label for="dateOfBirth">Date of Birth</label>
                                <input type="date" class="form-control" id="dateOfBirth" name="dateOfBirth">
                            </div>
                        </div>

                        <div class="form-group">
                            <label for="email">Email</label>
                            <input type="email" class="form-control" id="email" name="email" placeholder="Email">
                        </div>

                        <div class="form-group">
                            <label for="phone">Phone Number</label>
                            <input type="tel" class="form-control" id="phone" name="phone" placeholder="Phone Number">
                        </div>

                        <button type="submit" class="btn btn-primary btn-block">Submit</button>
                    </form>
                    <div id="output"></div>
                </div>
            </div>      
        </div>
  </body>
</html>

```

#### JavaScript
 
```
<script>

  function preventFormSubmit(){
    var forms=document.querySelectorAll('form');
    for (var i=0;i<forms.length;i++){
      forms[i].addEventListener('submit',function(event){
        event.preventDefault();
      });
    }
  }
window.addEventListener('load',preventFormSubmit);

function handleFormSubmit(formObject){
  google.script.run.processForm(formObject);
  document.getElementById("myForm").reset();
}


</script>


```


