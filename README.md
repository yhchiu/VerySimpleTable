VerySimpleTable
===============

A very lightweight Javascript-Bootstrap table generator with server-side paging, sorting and filtering. Requires JQuery but could be rewritten to not use JQuery without too much effort. It uses native Bootstrap 3 components for styling.

### How to use it
(1) Create an empty HTML element where you want your table and take a note of the ID
(2) Add some Javascript to the bottom of your page. For example:

```
<script>
    $(document).ready(function() {
        var grid = new VerySimpleTable();
        grid.initalise({
            callUrl: 'http://hostname/json/pathToCall',
            editUrl: '#',
            deleteUrl: '#',
            container: 'grid',
            columns: ['col1', 'col2', 'col3'],
            postData: {}
        });
    });
</script>
```

Note that the first argument passes to initialise() is a URL that returns JSON when POSTed to. The second and third are  optional URLs to edit/delete the entity (the first column will be passed as a parameter). The fourth is the ID of the element that we created earlier and the third is an array of column names. The column names should used underscored_names. The final parameter is an object that will be JSON encoded and sent as the POST payload.

(3) Ensure that the URL passed to the script returns JSON in the following format when POSTed to:
  
```
{"status":"success","data":[{"id":"1","name":"Test User","email":"test@test.com"},{"id":"2","name":"Test Client","email":"test@client.com"}],"count":2}
```

(4) Ensure that your server uses the following GET properties to reshape the JSON output in the obvious ways: "skip", "take", "sortBy", "direction" and "filter".
