---
title: Project Phase 3
layout: doc
---



# Project Phase 3: Convergent Design




## Functional Design




### `Mapping [Item]`:


- **Purpose**: Provide a map display where users can zoom in/out on the map and view user-uploaded information based on location.
- **Operational principle:** User zooms into map, finds a location, and clicks on it to view user-uploaded information and light pollution statistics specific to that location.
- **State**:
   - items: list Item
   - heatmapVisible: one Boolean
- Actions: (most of these concepts can be done on the frontend)
   - click(x: Number, y: Number): view an item (enlarge information on pin)
   - unclick(x: Number, y: Number): unview a item
   - zoom(zoomAmount: Number): zooms in and out of the map
   - scroll(scrollX: Number, scrollY: Number): scrolls across the map
   - toggleHeatmap(): turn heatmap on and off
   - findDarkSpot(threshold: Number, radius: Number): Guides a user to any location within a certain threshold of light pollution, within a certain distance from the user.


### Posting:


- **Purpose**: Provide a feed of user-uploaded information in a convenient scrollable format with customizable filters.
- **Operational principle:** As the user scrolls through the feed, new sky observations that are close to the user’s location appear. Users can choose to filter sky observations based on location.
- State:
   - id: one ObjectId
   - author: one ObjectId
   - location?: Tuple (x: one Number, y: one Number)
   - description: one String
   - hashtag: one `list[String]`
   - image: one String
   - likes: one Number
   - posts: list Post
- Actions:
   - createPost(author: ObjectId, description: String, image: String, location?: Tuple(x: Number, y: Number)): creates a post and returns a postId: String
   - deletePost(user: ObjectId, postId: ObjectId): checks that user is the author of the post and if so, deletes the post
   - editPost(user: ObjectId, postId: ObjectId, description: String)
   - viewPosts(key: String, value: String): returns a list of posts with `Post[key]=value`
   - getLikes(postId: ObjectId): returns the number of likes
   - boostPost(postId: ObjectId): moves the post earlier in posts by 2 spots
   - getHashtags(postId: ObjectId) returns the hashtags from the post


### Foruming[Author, Comment]:


- **Purpose**: To bring together communities with similar interests.
- **Operational principle:** Users look at other users’ messages and can reply or add a message for a new topic.
- **State**:
   - Id: one ObjectId
   - Channels: list Channel
   - Channel:
       - author: ObjectId
       - title: String
       - description: String
       - comment: list Comments
- **Actions**:
   - createChannel(author: objectId, title: String, description: String, []): author creates channel with title and description, empty comments initially. Returns channelId.
   - deleteChannel(author: objectId, channelId: objectId): if author == channelId.author, delete channel
   - getChannel(channelId: objectId): get channel with channelId.
   - addCommentToChannel(channel: objectId, comment: objectId): add comment to channel.comments
   - deleteCommentOnChannel(channel: objectId, comment: objectId): delete Comment from channel.comment
   - editChannelDescription(channel: channelId): edit channel.description
   - editChannelTitle(channel: Channel): edit channel.title


### Tracking:


- **Purpose**: Shows users what events are viewable from certain locations.
- **Operational Principle**: Users can click a tab which will bring them to a list of observable space objects and clicking on an object will give the user updated information about its current location and tips on how to spot it.
- **State**:
   - userLocation: one Tuple (x: one Number, y: one Number)
   - currentTime: one Date
   - Event:
       - time: one Date
       - location: Tuple (x: one Number, y: one Number)
       - description: one String
       - viewable: one Boolean
- **Actions:**
   - viewEvents(): lets the user view which astronomy related events are viewable in their area.
   - postEvent(time: Date, location: Tuple (x: Number, y: Number), description: String, viewable: Boolean): post an event which will show up to users who are close by.


### Rewarding [User, Post]


- **Purpose**: Reward and boost users that make frequent, high-quality posts so that beginner users know of experienced users to reach out to.
- **Operational Principle:** Based on the frequency of the posts and the number of likes, users can earn badges beside their names, which show up next to their names when they post.
- **State**:
   - badges: dictionary of lists `{User.objectId: [Badge, points]}`
   - Badge:
       - name: one String e.g. “Rising Stargazer Badge”
       - logo: one String //links to an image
       - threshold: one Number
       - hashtags: list string e.g. [“Mars”, “Venus”, “Orion”] //hashtags will be used to relate posts to specific badges.
   - boost: one Boolean
- **Actions**:
   - addPoints(userId: ObjectId, badgeId: ObjectId, pointsToAdd: Number): adds pointsToAdd to a User’s progress towards that badge.
   - earnBadge(threshold: Number, badge: Badge): add Badge to badges if points is above threshold
   - setBoost(likes: Number): if likes is above a certain threshold, set boost to True
   - addPointsHashtag(postId: ObjectId): goes through posts’ hashtag list and adds points to the progress related badges.


## Synchronizations




**app** Enlighten




**include** Authenticating [Username, Password] include `Sessioning [User] include Mapping [Post] include Posting [User] include Foruming [User, Post] include Tracking [User] include Rewarding [User]`




**sync** boostPosts(post: objectId):


- likes = Posting.getLikes(postId: ObjectId)
- Rewarding.setBoost(likes: Number)
- Posting.boostPost(postId: ObjectId)


**sync** postToFeed(u: User, description: string, image: string, location: string, hashtag: list string):


- postId = Posting.createPost(u, description, image, location) // create post with location & hashtag
- Rewarding.addPoints(u._Id, postId, 1)
- Rewarding.addPointsHashtag(postId)


**sync** postToChannel(u: User, description: string, image: string, channelId: objectId):


- postId = Posting.createPost(u, description, image) // create post without location
- Foruming.addCommentToChannel(channelId, postId) // add the post to channel
- Rewarding.addPoints(u._Id, channelPostBadgeId, 1)


**sync** deletePostFromChannel(u: User, postId: objectId, channelId: objectId):


- Foruming.deleteCommentToChannel(channelId, postId) // add the post to channel
- Posting.deletePost(u, postId) // create post without location


## Dependency diagram




<figure>
                     <img src="https://res.cloudinary.com/df2rp6zoo/image/upload/v1732150342/tvgpk7lvzc4ygesbkde1.png" alt="">
                     <figcaption></figcaption>
                 </figure>




## **Wireframes**


https://www.figma.com/design/XiyPgO5MwFG2t2EEgxdT1V/Enlighten-P3?node-id=0-1&node-type=canvas&t=z1IjS1zHZxC3R8U8-0




## **Heuristic Evaluation**




### Usability criteria


- **Discoverability**: The interface is intuitive and simple. The map uses Google Maps’s API, which the vast majority of users will be familiar with. The feed emulates the standard social media feed, with a series of posts that they can scroll down. The navbar is prominent on the left so that users know how to find different pages.
- **Error Tolerance:** If the wrong pin is clicked on the map, it is easy to click away. However, if the user clicks on the wrong celestial object on the tracker page, such as Mars instead of the Big Dipper, there is no back button to return to the previous page. Instead, the user has to click on the navbar again.


### Physical heuristics


- **Fitt’s Law:** As mentioned above, the navbar is far away from where information is displayed. While this prevents users from accidentally clicking on the navbar and is the best choice visually, it would be ideal for users to only need to use the navbar to switch to a different page. In other words, the user should be able to traverse within each page without having to click on the navbar.
- **Accelerators:** There are currently no features to speed up usage for experienced users. One possible accelerator would be favoriting spots on the map, so that users have a shortcut to locating those spots.


### Linguistic level


- **Speak User’s Language:** The language used in the wireframes is easily understandable. Descriptions of celestial objects are intentionally kept simple for beginner stargazers.
- **Information Scent:** In the forum wireframe, the text box has the default message “Type and share something with group”. This tells users that they can participate in the forum and encourages them to interact with other users.


## **Visual Design Study**




### Color




<figure>
                     <img src="https://res.cloudinary.com/df2rp6zoo/image/upload/v1732150343/oldcfi9qyxpnnjaailo4.png" alt="">
                     <figcaption></figcaption>
                 </figure>




### Typography




<figure>
                     <img src="https://res.cloudinary.com/df2rp6zoo/image/upload/v1732150344/xmuq80ibrgdco43omlvw.png" alt="">
                     <figcaption></figcaption>
                 </figure>




## **Implementation Plan**


Order of implementing concepts: Posting, Rewarding, Mapping, Foruming, Tracking


Tasks:


- Posting
   - Backend: Tina. Deadline 11/25
   - Frontend: Tina. Deadline 11/25
- Rewarding
   - Backend: Johanna. Deadline 11/25
   - Frontend: Johanna. Deadline 11/25
- Mapping
   - Backend: Francisco. Deadline 12/3
   - Frontend: Francisco. Deadline 12/3
- Foruming
   - Backend: Helena. Deadline 12/3
   - Frontend: Helena. Deadline 12/3
- Tracking
   - Backend: Francisco. Deadline 11/25
   - Frontend: Francisco. Deadline 11/25
- User testing
   - Tina, Johanna, Helena each do two, Francisco does one. Deadline 12/10


## Contingency Plan


We plan to reward badges to users for both posting and participating in forums. However, if we don’t have time, we can reward badges only for posting. We can also create less badges. In addition, since tracking doesn’t rely on any other concepts, it can be expanded or simplified as needed. For example, we can track just planets and moons rather than planets, moons, stars, and constellations. Lastly, if adding the heatmap proves too complicated, we can display the regular map. We aim to flexibly add or change these features after each TA and group meeting.




