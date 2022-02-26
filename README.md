# Project: Connect

## Usage
Create a django environment named djangoenv with: `conda create -n djangoenv python=3.7`
Activate djangoenv with: `conda activate djangoenv`
Install django using: `conda install -c anaconda django`

With all installations complete, you can now run the server. Make sure you are in the Project03 root folder.

Run the server **locally** with `python manage.py runserver localhost:8000` and go to localhost:8000/e/mathak1/ on your browser.

Run the server on **mac1xa3.ca** with `python manage.py runserver localhost:10007` and go to mac1xa3.ca/e/mathak1/ on your browser.

Begin by creating an account, which is explained at objective 1 below.

## Objective 01
**Description:** This feature is displayed in signup.djhtml which is rendered by signup_view in login/views.py.

Signup.djhtml uses the django UserCreationForm to display a form for creating a new user. Submitting the form sends a post request to /e/mathak1/signup/ which is handled by signup_view, and creates a new UserInfo entry with the inputted username and password.

## Objective 02
**Description:** This feature is displayed in social_base.djhtml which is then rendered by either messages_view, people_view or account_view, depending on the current template being used, all of which extend social_base.djhtml.

All of the three views listed above pass the currently logged in UserInfo object to the social_base.djhtml template, which then displays the UserInfo object's attributes on the user information column on the left, no matter which template you are in.

## Objective 03
**Description:** This feature is displayed in account.djhtml and is rendered by account_view in social/views.py.

This feature utilizes the django PasswordChangeForm() and a custom made UserInfoForm() from social/models.py. Submitting a form sends a post request to /e/mathak1/social/account/ which is handled by account_view, which then changes the password, or attribute values of the currently logged in UserInfo object.

**Exceptions:** If the user is not authenticated, they are redirected to login.djhtml.

## Objective 04
**Description:** This feature is displayed in people.djhtml and rendered by people_view in social/views.py.

This feature displays users who are not friends of the current logged in user. The amount of users displayed is limited, and is determined by a session variable that is initiated at 1.

In addition, upon pressing the "More" button, a post request from people.js is sent to /e/mathak1/social/moreppl/ which is then handled by more_ppl_view, which increases the session variable containing the limit of users displayed by 2.

**Exceptions:** If the user is not authenticated, they are redirected to login.djhtml.

## Objective 05
**Description:** This feature is displayed in people.djhtml and rendered by people_view in social/views.py.

People.djhtml displays friend requests received by the currently logged in user on the right column. Additionally, all of the users displayed in objective04 are displayed with a friend request button. People.djhtml configures this friend request button so its id contains the id of the user receiving the friend request.

Upon pressing the friend request button, a post request from people.js is sent to /e/mathak1/social/friendrequest/ and is handled by friend_request_view, which creates a new entry to the FriendRequest model which was sent form the currently logged in user, and sent to the receiving user given their user id.

**Exceptions:** Returns a 404 error if the post data doesn't contain any friend request id.

## Objective 06
**Description:** This feature is displayed in people.djhtml and rendered by people_view in social/views.py.

People.djhtml displays all friend requests received by the currently logged in user on the right column, each with accept and decline buttons. The id of each of these buttons contains the id of the user who sent the friend request.

Pressing either of the buttons sends a post request from people.js to /e/mathak1/social/acceptdecline/ and is handled by accept_decline_view. The FriendRequest entry is then deleted, and if the accept button was pressed, both of the users' UserInfo is updated to add each other as friends.

**Exceptions:** Returns a 404 error if the post data doesn't contain any accept/decline button id.

## Objective 07
**Description:** This feature is displayed in messages.djhtml and rendered by messages_view in social/views.py.

Messages.djhtml displays all of the friends of the currently logged in user on the right column.

**Exceptions:** If user is not authenticated, page is redirected to login.djhtml.

## Objective 08

**Description:** This feature is displayed in messages.djhtml and rendered by messages_view in social/views.py.

Messages.djhtml displays a field for submitting posts in the top middle column of the page. Pressing the submit button on a post sends a post request from messages.js to /e/mathak1/social/postsubmit/ which is handled by post_submit_view. The post request contains the text that was written in the post field mentioned above. After, post_submit_view creates a new Post entry with the data received from the post request as content.

**Exceptions:** Returns a 404 error if no content was received with the post request.

## Objective 09

**Description:** This feature is displayed in messages.djhtml and rendered by messages_view in social/views.py.

Messages.djhtml displays all of the existing posts, ordered from newest to oldest, in the middle column of the page. The amount of posts displayed is limited, and is determined by a session variable that is initiated at 1.

In addition, upon pressing the "More" button, a post request from messages.js is sent to /e/mathak1/social/morepost/ which is then handled by more_post_view, which increases the session variable containing the limit of posts displayed by 2.

**Exceptions:** If the user is not authenticated, they are redirected to login.djhtml.

## Objective 10
**Description:** This feature is displayed in messages.djhtml and rendered by messages_view in social/views.py.

All posts displayed in the middle column have a "Like" button as well as a like counter. The id of each like button contains the id of the post it is associated with. Pressing a like button submits a post request from messages.js to /e/mathak1/social/like/ which is then handled by like_view.

like_view querys the Post entry that was liked, given the entry's id from the post request, and then adds the currently logged in UserInfo object to the Post object's 'likes' attributes.

**Exception:** Returns a 404 error if no id was received from the post request.

## Objective 11
**Description:** This feature is a test database created to test all the objectives listed above. The db.sqlite3 is in the root of this folder. The migrations folder can be found at (starting from the root folder) social/migrations.

Five users were created:

 1. Username: Test1/ Password: password1
 2. Username: Test2 Password: password1
 3. Username: Test3 Password: password1
 4. Username: Test4 Password: password1
 5. Username: Test5 Password: password1

**Note:** below are examples of entries in the database which were used to test that each feature and objective works. The objective being shown is **bolded**.

**Examples**:
-  All of the users were created using the features from **objective 01.**
- When logged in, all of the users have their information displayed on the left column using the features from **objective 02** and **objective 03**.
- Test3 and Test4 both have received a friend request from Test5, sent through the friend request button on the people list, and displayed on their friend request list using features from **objective 04** and **objective 05**.
- Test5 and Test2 are friends, as well as Test2 and Test3, using features from **objective 06**. You can also see that Test5 and Test3 are displayed under Test2's friends list, using features from **objective 07**.
- Test4 and Test3 have created posts which are displayed on the messages page, using features from **objective 08** and **objective 09**.
- Test3, Test2, and TestUser 5 have all liked Test3's post. Test5 has also liked Test4's post. This used features from **objective 10**.