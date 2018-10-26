# codefundo
## HUB Implementation
* HUB is a resource sharing platform where merchants can register and donate per the requested resources.
* It is realised in the form of a webapp, built using Django. The Database utilised is Azure MySQL.
* It employs the admin, user model. The users are merchants willing to provide resources and the admin is a disaster relief organization.
* It employs a payment platform for 
#### The following is our SQL Model, for storing and querying data.

TABLE USER stores a Merchant's details
``` python
class Users(models.Model):
    FOOD = 'FOOD'
    CLOTHING = 'CLOTHING'
    MISC = 'MISC'
    NULL = 'NULL'

    Product_Types_choices = (
        (FOOD, 'Food'),
        (CLOTHING, 'Clothing'),
        (MISC, 'Miscellaneous'),
        (NULL, 'Nothing'),
    )
    
    name = models.CharField(max_length=100)
    email = models.EmailField(max_length=150, primary_key=True,unique=True)
    phone=models.CharField(max_length=10)
    prod_type = models.CharField(max_length=10,choices = Product_Types_choices, default=NULL)
    paypal_id = models.CharField(max_length=250)
    password = models.CharField(max_length=150)
    user_type = models.CharField(max_length=150)
 ```
 TABLE PRODUCT stores the list of products/services offered by the merchants
 ```python
 class Product_List(models.Model):
    FOOD = 'FOOD'
    CLOTHING = 'CLOTHING'
    MISC = 'MISC'

    Product_Types_choices = (
        (FOOD, 'Food'),
        (CLOTHING, 'Clothing'),
        (MISC, 'Miscellaneous'),
    )
    
    email = models.ForeignKey('Users', on_delete=models.CASCADE)
    user = models.CharField(max_length=100)
    prod_type = models.CharField(max_length=10, choices = Product_Types_choices)
    product = models.CharField(max_length=200,blank=False)
    price = models.PositiveIntegerField()
    qty = models.PositiveIntegerField()
   ```
 Django's default DB is set to Azure MySQL
 ```python
 DATABASES = {
    'default': {

        'ENGINE': 'django.db.backends.mysql',

        'NAME': 'indigocodefundo',                     

        'USER': 'agchaitanya',                     

        'PASSWORD': '',                  

        'HOST': 'localhost',                     

        'PORT': '3306',

    }
}
```

