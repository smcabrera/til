# Posting to rails with javascript

I'm using the following javascript

```javscript
$(".ingredient-amount-field").change(function(){
  var ri_id = $(this).data('id');
  data = {
    amount : $(this).val()
  }
  $.post("/recipe/" + recipe_id + "/recipe_ingredients/"+ri_id, data, function(data){
     // Plus create the route and controller action for creating a recipe
  })

})
```

(it's not quite correct but you get the idea...)

To make a post http request to a rails controller action via ajax. This is a super userful pattern and Michael says it'll come up a lot. I'm sure it will. Definitely something to practice and perfect more.

The data-id there is an html attribute that a form input has. With erb you can dynamically generate that attribute by passing it in through rails. This is an important concept to get generally when it comes to working with javascript and rails. These dynamically generated data attributes are clutch for creating a bridge between rails and javascript.


