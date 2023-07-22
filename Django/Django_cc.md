# Django:
- Django is a high-level Python web framework which is based on MVT architecture.

## MVT (Model View Template):
- The MVT is an design pattern that separates an application into three main logical componentsL
  - **Model:**
    - The Model responsible to handle database. It is a data access layer which handles the data.
    - Written in Python (Need knowledge about Databases)
  - **View:**
    - The user can send request by interacting with template, the view handles these requests and sends to Model then get appropriate response from the Model, sends response to template. It works as a mediator between Template and Model.
    - It may also have required logics (Python)
  - **Template:**
    - It represents how data should be presented to the application user. User can read or write the data from template. Basically it is responsible for showing end user content, we can say it is user interface.
    - It may consists of HTML, CSS, JS mixed with Django Template Language.

<img width="1338" alt="MVT" src="https://github.com/IshaanAdarsh/TIL/assets/100434702/2795db0a-6c70-48b7-bdf5-e1023228f439">
