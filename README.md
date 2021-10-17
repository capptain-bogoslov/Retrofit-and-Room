# Retrofit-and-Room
Fieldcode Task - 17/10/2021
==================================
Developed by : Theologos Batsioulas 


Description
------------
The FieldcodeTask App is doing the following :
1. Get data (only Users and Todos) from the web-service  https://jsonplaceholder.typicode.com/ with the use of Retrofit Library
2. Creates and Stores the data locally in a Room Database (2 Entities User and Task)
3. Manipulate the data (insert, update, delete) inside the Room Database from a Repository
4. Observe the data changes with the use of LiveData in a ViewModel
5. Post data in the web-service with the use of Retrofit Library (@POST)
6. Displays data inside Fragments in Recycler Views (1 Activity - 3 Fragments)


Use Cases
-----------
1. App has only one Activity with 3 Fragments that are created inside
2. Start - UsersFragment (list of Users from web-service). 1 RecyclerView and 1 FloatingActionButton
2.1. User can press in any RecyclerView item and will see the Tasks for the chosen user in TasksListFragments
b. User can press FloatingActionButton to Post something (it has no business logic but i chose to present the capability to use a POST method with Retrofit)
3. in TasksListFragments are displayed the Tasks of the spesific user that is chosen in UsersFragment. It has 1 RecyclerView and 1 FloatingActionButton
a. in any RecyclerView item and can update or delete the Task in AddOrEditFragment
b. User can press FloatingActionButton to Add a new Task to this User in Database
4. In AddOrEditFragment it has 1 EditText for title, 1 Editext for body (visible only in POST use case), 1 spinner for completed status (boolean), 1 button for Save, 1 button for Delete. According the type that get from safeArgs it has different functions
a. POST - User can Post something in web service. Only title, body and Post button are visible
b. ADD - User can Add a Task in the chosen user. Visible are title, completed, Save button layouts
c. UPDATE - User can update an existing Task - Only body not visible


Packages - Classes - Description
------------------------
com.task.fieldcodetask
		AddOrEditFragment (Fragment Class that Add, Update, Delete a Task or Post a post from User)
		MainActivity (Main App Activity that setups Navigation Controller)
		TaskApplication (Application class for Room database that subclass Application and gets Database
		TaskRepository (Repository Class that handles data with Dao classes and gives access to data to ViewModel)
		TasksFragment (Fragment Class that dislpays the Tasks for the chosen User)
		UsersFragment (Fragment Class that displays the List of Users)
	adapters -	
		TaskListAdapter (RecyclerViewAdapter for TaskListFragment)
		UserListAdapter(RecyclerView Adapter for UsersFragment)
	database -
		Post (Data class to create a Post for use in the @POST API with Retrofit)
		Task (Entity Class for Task)
		TaskDao (DAO class that provide access to data for Task)
		TaskDatabase (Room Database Class amd main access point with the DB)
		User (Entity Class for User)
		UserDao (DAO class that provide access to data for Task)
	model -
		ViewModel.kt (ViewModel Class and Factory class that ensure the data are separated from UI. talks with the UI)
	network -	
		TaskApiService.kt (Service Class that build Retrofit and Moshi Objects and defines how Retrofit will get data)
				

Design Patterns
----------------
The design Patetrn used is Model-View-ViewModel(MVVM) and is implemented as below 

					---------------------
					| Activity/Fragments|
					| MainActivity,     |
					| UsersFragment     |
				  | TaskListFragments |
					---------------------
					    	     |
						         |
					-----------------------
					| TaskModel(LiveData) |	   					
					|-ViewModel Class-    |	
					-----------------------
						         |
						         |
					-----------------------
					|     TaskRepository  |
					-----------------------
						         |
						         |
				      ------------------------------
		      		|	                 				   |
			      	|	                 				   |
			-------------------	    -----------------------------
			| UserDao, TaskDao|			| TaskApiService (Retrofit) |	
			-------------------			-----------------------------
			      	|	                  					|
				      |                 						|
			=================			===========================================
			|| Room Database ||			|| https://jsonplaceholder.typicode.com/ ||
			==================			==========================================
			

Libraries used
--------------------------------
1. Retrofit (REST API for get and post data)
2. Room (Creating and store data locally in Room database)
3. Moshi (Converting JSON Objects to Kotlin Objects)
4. Navigation Component (use of Navigation Graph to navigate between Fragments and use safeArgs to pass Arguments)



Getting Started
---------------

1. Download and run the app.
2. Network Connection must be availabe


Not done
--------------

1. Unit Testing
2. Sorting of data dislpayed in Fragments
3. UI details
4. Bussiness Logic
