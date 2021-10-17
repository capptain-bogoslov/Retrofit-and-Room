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
2. (UsersFragment) (list of Users from web-service). 1 RecyclerView and 1 FloatingActionButton
3. (UsersFragment)User can press in any RecyclerView item and will see the Tasks for the chosen user in TasksListFragments
4. (UsersFragment)User can press FloatingActionButton to Post something (it has no business logic but i chose to present the capability to use a POST method with Retrofit)
5. (TasksListFragment) (Tasks of the chosen user in UsersFragment). 1 RecyclerView and 1 FloatingActionButton
6. (TasksListFragment)User can press in any RecyclerView item and can update or delete this Task in AddOrEditFragment
7. (TasksListFragment)User can press FloatingActionButton to Add a new Task to this User in Database
8. (AddOrEditFragment) 1 EditText for title, 1 Editext for body (visible only in POST use case), 1 spinner for completed status (boolean), 1 button for Save, 1 button for Delete. According the type that get from safeArgs it has different functions
9.  (AddOrEditFragment) POST - User can Post something in web service. Only title, body and Post button are visible
10. (AddOrEditFragment) ADD - User can Add a Task in the chosen user. Visible are title, completed, Save button layouts
11. (AddOrEditFragment) UPDATE - User can update an existing Task - Only body not visible


Packages - Classes - Description
------------------------
1. AddOrEditFragment (Fragment Class that Add, Update, Delete a Task or Post a post from User)
2. MainActivity (Main App Activity that setups Navigation Controller)
3. TaskApplication (Application class for Room database that subclass Application and gets Database)
4. TaskRepository (Repository Class that handles data with Dao classes and gives access to data to ViewModel)
5. TasksFragment (Fragment Class that dislpays the Tasks for the chosen User)
6. UsersFragment (Fragment Class that displays the List of Users)
7. (adapters) TaskListAdapter (RecyclerViewAdapter for TaskListFragment)
8. (adapters) UserListAdapter(RecyclerView Adapter for UsersFragment)
9. (database) Post (Data class to create a Post for use in the @POST API with Retrofit)
10. (database) Task (Entity Class for Task)
11. (database) TaskDao (DAO class that provide access to data for Task)
12. (database) TaskDatabase (Room Database Class amd main access point with the DB)
13. (database) User (Entity Class for User)
14. (database) UserDao (DAO class that provide access to data for Task)
15. (model) ViewModel.kt (ViewModel Class and Factory class that ensure the data are separated from UI. talks with the UI)
16. (network) TaskApiService.kt (Service Class that build Retrofit and Moshi Objects and defines how Retrofit will get data)
				

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
					|   TaskRepository    |
					-----------------------
						   |
						   |
				------------------------------
		      		|	                      |
			      	|	                      |
			-------------------	    -----------------------------
			| UserDao, TaskDao|	    | TaskApiService (Retrofit) |	
			-------------------	     -----------------------------
			      	|	                  	|
				|                 		|
			=================	===========================================
			|| Room Database ||	|| https://jsonplaceholder.typicode.com/ ||
			==================	==========================================
			

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
