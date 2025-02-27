# Built-in Field Options in Django Models

1. `null`: It can contain either True or False. If True, Django will store empty values as NULL in the database. Default is False.
   Avoid using null on string-based fields such as CharField and TextField. If a string-based field has null=True, that means it has two possible values for "no data: NULL, and the empty string.
   Example: `null=True/False`

2. `blank`: It can contain either True or False. If True, the field is allowed to be blank. This is different than null. null is purely database-related, whereas blank is validation-related. If a field has blank=True, form validation will allow entry of an empty value. If a field has blank=False, the field will be required.
   Default is False.
   Example: `blank=True/False`

3. `default`: The default value for the field. This can be a value or a callable object. If callable it will be called every time a new object is created.
   Example: `default='Not Available'`

4. `verbose name`: A human-readable name for the field. If the verbose name isn't given, Django will automatically create it using the field's attribute name, converting underscores to spaces.
   Example: `verbose_name='Student Name'`

5. `db_column`: The name of the database column to use for this field. If this isn't given, Django will use the field's name.
   Example: `db_column='Student Name'`

6. `primary_key`: If True, this field is the primary key for the model. If you don't specify primary_key=True for any field in your model, Django will automatically add an AutoField to hold the primary key.
   Example: `primary_key=True`

7. `unique`: If True, this field must be unique throughout the table. This is enforced at the database level and by model validation. If you try to save a model with a duplicate value in a unique field, a `django.db.IntegrityError` will be raised by the model's save method.

8. `IntegerField`: An integer. Values from -2147483648 to 2147483647 are safe in all databases supported by Django.
   Example: `roll = models.IntegerField()`

9. `BigIntegerField`: A 64-bit integer, much like an IntegerField except that it is guaranteed to fit numbers from -9223372036854775808 to 9223372036854775807.
   Example: `mobile = models.BigIntegerField()`

10. `AutoField`: An IntegerField that automatically increments according to available IDs. You usually won't need to use this directly; a primary key field will automatically be added to your model if you don't specify.
    Example: `stuid = models.AutoField()`

11. `FloatField`: A floating-point number represented in Python by a float instance.

12. `CharField`: A string field, for small- to large-sized strings. For large amounts of text, use TextField. CharField has one extra required argument: max_length.
    Example: `first_name = models.CharField(max_length=30)`

13. `TextField`: A large text field. If you specify a max_length attribute, it will be reflected in the Textarea widget of the autogenerated form field. However, it is not enforced at the model or database level.

14. `URLField`: A CharField for a URL, validated by URLValidator. If you don't specify max_length, a default of 200 is used.
    Example: `partnersite = models.URLField()`

15. `BinaryField`: A field to store raw binary data. It can be assigned bytes, bytearray, or memoryview. By default, BinaryField sets editable to False, in which case it can't be included in a ModelForm. BinaryField has one extra optional argument: max_length.
    Example: `profile_img = models.BinaryField()`
