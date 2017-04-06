Hi, here I explain in details the step-by-step procedure on how I install the Yii framework and
the CRUD Generator provided by Gii Tool. Next, I explain how the program works in a simple way.

PART A: How I Install the Yii Framework and CRUD Generator
PART B: How the Program Works


My system:
==========
OS: Windows 7
Local server: XAMPP
Database: SQLite
Framework: Yii 2.0
Text editor: Sublime Text


PART A: How I Install the Yii Framework and CRUD Generator
==========================================================

Step 1: Yii Framework Installation
==================================

i)	Download and install the Yii framework via archive file.
ii)	Choose 'Yii 2 with basic application template'.

Download Web Link: http://www.yiiframework.com/download/
Screenshot: \SS\A\001.jpg

iii)Next, extract the .zip file (yii-basic-app-2.0.11.zip) to the Web-accessible folder (eg: \htdocs).
iv)	After extraction, the project folder should have named 'basic'.

Directory installation: C:\xampp\htdocs\yii-basic-app-2.0.11\yii-basic-app-2.0.11\basic\
Screenshot: \SS\A\002.jpg


Step 2: SQLite Server Installation
==================================

i)	For Windows, choose 'Precompiled Binaries for Windows'.
ii)	Download the 'sqlite-dll-win32-x86-3180000.zip' and 'sqlite-tools-win32-x86-3180000.zip' files.

Download Web Link: https://sqlite.org/download.html
Screenshot: \SS\A\003.jpg

iii)Next, extract both .zip files to a common folder named 'sqlite' and put in any desired directory.
iv)	The folder should have the files as shown in the screenshot \SS\A\004.jpg.

Directory installation: C:\xampp\htdocs\yii-basic-app-2.0.11\yii-basic-app-2.0.11\sqlite\
Screenshot: \SS\A\004.jpg


Step 3: Create A Database
=========================

i)	In the 'sqlite' folder, open the 'sqlite3.exe' application.
ii)	To create a new database, type in the console '.open myDatabase.db'.

Screenshot: \SS\A\005.jpg


Step 4: Create A Table
======================

i)	Create a table named 'Task' by typing in the following SQL command:

CREATE TABLE Task (
id 		INT 	PRIMARY KEY 	NOT NULL,
name 	TEXT 					NOT NULL
);

Screenshot: \SS\A\006.jpg


Step 5: Configure Database Connection
=====================================

i)	Open the project folder 'basic' in any desired text editor (eg: Sublime Text).
ii)	Navigate to the database configuration file (db.php) to configure the database connection.
iii)If using SQLite server, use the following SQLite configuration command:

''dsn' => 'sqlite:location\to\sqlite\file.db

or as shown in the screenshot \SS\A\007.jpg.

Leave everything else as it is.


Step 6: Configure Validation Key
================================

i)	Up to this point, if you were to test opening the project in the browser, it will display an error page as shown in \SS\A\008.jpg.
ii)	This is because a cookie validation key is required.
iii)Navigate to the web configuration file (web.php) to configure the cookie validation key.
iv)	Under the variable '$config', insert any secret key in the 'cookieValidationKey' (eg: 'myKey') as shown in \SS\A\009.jpg.

Leave everything else as it is.

v)	If you were to open the project in the browser at this point, it will show you
the home page of the web as shown in \SS\A\Yii_home.jpg.


Step 7: Create A Model Using The Model Generator Provided by Gii Tool
=======================================================================

i)	In the URL browser, navigate to the Gii Tool home page as shown in \SS\A\Gii_home.jpg

URL: http://localhost/yii-basic-app-2.0.11/yii-basic-app-2.0.11/basic/web/index.php?r=gii

ii)	Click the 'Start' button under Model Generator to create a new model.
iii)In the 'Table Name' textfield, type in the table name (eg: 'Task').
iv)	In the 'Model Class' textfield, type in the model name (eg: 'Task').

Refer to screenshot: \SS\A\010.jpg

Leave everything else as it is.

v)	Click the button 'Preview' and then 'Generate'. 
vi)	If everything work perfectly, the code will be generated successfully. Else, give permissions to write files in the project folder.

vii)A file named 'Task.php' should be created in \basic\models\


Step 8: Implement A CRUD Operation Using The CRUD Generator Provided by Gii Tool
===============================================================================

i)	Click 'CRUD Generator' to implement a CRUD operation.
ii)	In the 'Model Class' textfield, type in the model path (eg: 'app\models\Task').
iii)In the 'Search Model Class' textfield, type in the search model path (eg: 'app\models\TaskSearch').
iv)	In the 'Controller Class' textfield, type in the controller path (eg: 'app\controllers\TaskController').

Refer to screenshot: \SS\A\011.jpg

Leave everything else as it is.

v)	Click the button 'Preview' and then 'Generate'. 
vi)	If everything work perfectly, the code will be generated successfully. Else, give permissions to write files in the project folder.

vii)The following files should be created in:
\basic\controllers\
	TaskController.php
\basic\models\
	TaskSearch.php
\basic\views\task\
	_form.php
	_search.php
	create.php
	index.php
	update.php
	view.php

viii)This will create a new CRUD system.

ix)	To test the system, navigate to the index page:
http://localhost/yii-basic-app-2.0.11/yii-basic-app-2.0.11/basic/web/index.php?r=task/index

Refer to screenshot: \SS\A\Task_index.jpg

Step 9: Add A Field
===================

i)	Navigate to \basic\views\task\ _form.php

ii)	Add a form field 'id' to ensure the id of the task can be inserted into the database since it is a required value and it is not auto incremented.

Screenshot: \SS\A\012a.jpg
			\SS\A\012b.jpg


Step 10: Add Rules
==================

i)	Navigate to \basic\models\Task.php

ii)	To add rules to the form fields, simply add the rules into the function rules, as shown:

public function rules()
    {
        return [
            [['id'], 'required'],
            [['id'], 'integer'],
            [['id'], 'unique'],
            [['name'], 'required'],
            [['name'], 'string'],
        ];
    }

Screenshot: \SS\A\013a.jpg
			\SS\A\013b.jpg


Step 11: Testing
================

i)	Test the system:
http://localhost/yii-basic-app-2.0.11/yii-basic-app-2.0.11/basic/web/index.php?r=task/index


PART B: How the Program Works
=============================

Create a task
=============

1.	On the index page, click the 'Create Task' button.
2.	This will redirect to the 'create' page.
3.	In the 'create.php' file, the line of code below will render _form.php file onto the 'create' page.

	<?= $this->render('_form', ['model' => $model, ]) ?>

4.	In the _form.php file, the first line of code below will display the field label and field textarea. The second line will display a submit button.

	<?= $form->field($model, 'id')->textarea(['rows' => 1]) ?>

	<?= Html::submitButton($model->isNewRecord ? 'Create' : 'Update', ['class' => $model->isNewRecord ? 'btn btn-success' : 'btn btn-primary']) ?>

5. 	Input id and name of the new task in the respective textarea as shown in \SS\B\001.jpg.
6.	Click the 'Create' button.
7.	The variable $model is passed to the 'TaskController.php' file in the function 'actionCreate' where a new Task model is created. 
8.	In the TaskController.php file, the line of code below will create a new Task.

	$model = new Task();

9.	The lines of code below will check whether the creation of the task is successful. If the creation is successful, the browser will be redirected to the 'view' page as shown in \SS\B\002.jpg. Else, it will render the 'create' page.

	if ($model->load(Yii::$app->request->post()) && $model->save()) {
        return $this->redirect(['view', 'id' => $model->id]);
    } else {
        return $this->render('create', [
            'model' => $model,
        ]);
    }

9.	The Task.php file is the model class of the table 'Task'.

10.	The function 'rules' below defines the rules and validate the user input as shown in \SS\B\003.jpg.

	public function rules()
    {
        return [
            [['id'], 'unique'],
            [['id', 'name'], 'required'],
            [['id', 'name'], 'string'],
        ];
    }


Read a task
===========

1.	In the index.php file, the line of code below add an ActionColumn to the gridview that displays buttons for viewing and manipulating the items.

	['class' => 'yii\grid\ActionColumn'],

2.	On the index page, in the last column of the row of the selected task, click on the 'View' icon as shown in \SS\B\004.jpg.
3.	It will redirect to the 'view' page using the task ID as the argument as shown in \SS\B\005.jpg.
4.	In the view.php file, the line of code below displays the attribute labels and values of the selected task.

	<?= DetailView::widget([
        'model' => $model,
        'attributes' => [
            'id',
            'name',
        ],
    ]) ?>

Update a task
=============

1.	On the index page, in the last column of the row of the selected task, click on the 'Update' icon as shown in \SS\B\006.jpg.
2.	It will redirect to the 'update' page using the task ID as the argument.
3.	In the update.php file, the line of code below will render _form.php file onto the 'update' page.

    <?= $this->render('_form', ['model' => $model, ]) ?>

4. 	Input id and name of the updating task in the respective textarea as shown in \SS\B\007.jpg.
5.	Click the 'Update' button.
6.	The variable $model is passed to the 'TaskController.php' file in the 'actionUpdate' function where the existing Task model is updated.
7.	In the TaskController.php file, the line of code below will find the model with the selected id.

	$model = $this->findModel($id);

8.	The lines of code below will check whether the update of the task is successful. If the update is successful, the browser will be redirected to the 'view' page as shown in \SS\B\008.jpg. Else, it will render the 'update' page.

		if ($model->load(Yii::$app->request->post()) && $model->save()) {
            return $this->redirect(['view', 'id' => $model->id]);
        } else {
            return $this->render('update', [
                'model' => $model,
            ]);
        }

Delete a task
=============

1. On the index page, in the last column of the row of the selected task, click on the 'Delete' icon as shown in \SS\B\009.jpg.
2. In the view.php file, the lines of code below will show a confirm message when any 'Delete' function is triggered as shown in \SS\B\010.jpg.

		<?= Html::a('Delete', ['delete', 'id' => $model->id], [
            'class' => 'btn btn-danger',
            'data' => [
                'confirm' => 'Are you sure you want to delete this item?',
                'method' => 'post',
            ],
        ]) ?>
        
3. If confirmed, the variable $model is passed to the TaskController.php file in the 'actionDelete' function where the selected task is deleted.