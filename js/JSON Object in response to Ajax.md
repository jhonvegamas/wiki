```JS
data = $.ajax({
    type: 'GET',
    url: 'url-to-service',
    async: false,
    dataType: 'json',
    data: {param1: name, param2:email},
    done: function(results) {
        // If result is not JSON
        // JSON.parse(results);
        return results;
    },
    fail: function( jqXHR, textStatus, errorThrown ) {
        console.log( 'Could not get posts, server response: ' + textStatus + ': ' + errorThrown );
    }
}).responseJSON;
```JS
