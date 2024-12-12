---
title: Project Phase 6
layout: doc
---


# Project Phase 6: User Testing & Final Release


## User Study


### User Study 1
During testing, the participant demonstrated clarity in general navigation and completion of core tasks, such as using the side navigation panel, creating and viewing posts on the map, and engaging with badges and forums. They quickly grasped searching posts by hashtags and understood how to review and track badges by accessing their profile. Interactions with the forum were also smooth, as the participant easily entered a forum and added comments. The participant also complimented the design of the app, commenting that the app is minimalistic but has all the necessary information, and is not overwhelming.
However, several points of confusion arose. The participant struggled to identify the “+” button on the home page, initially mistaking it for a star, suggesting issues with icon clarity. When asked to find the post with the most likes, the participant scrolled through posts manually instead of using the “sort by likes” feature, indicating that key filtering tools may not be sufficiently visible. In addition, locating space objects near the user’s location presented challenges: the participant couldn’t find the “find” button and did not initially understand that location services needed to be enabled. These issues highlight the need for improved signposting, more intuitive iconography, and clearer guidance around location-based features.
### User Study 2
The user generally completed tasks in a timely and efficient manner. However, there were some points of confusion.On the toggle heatmap task, he was able to find and click the button easily, but was confused for a moment because the brightness of the heatmap was too low for him to notice, so he had to turn the heatmap off and on again to tell that there was a difference. On the filtering task, the user scrolled through the posts to find one with the hashtag moon instead of using the hashtag filtering tool. On the badging task, the user was confused by the lack of a badges page and clicked through the options on the navbar before going to his profile.
During the debriefing, he stated that since he doesn’t have his contacts in, his eyesight is worse than usual, so he couldn’t tell when he turned on the heatmap. This brought up a good point that for visually impaired users, we might need to use brighter colors. He also stated that he scrolled through posts instead of using the filtering tool because he saw there weren’t many posts, and if there had been over a hundred, he would’ve looked for a filtering tool instead. This highlighted the need for populating the app with an amount of data proportionate to the size of the expected user base. Lastly, for the badging task, the user stated that he was on autopilot and clicked through the navbar on instinct. This indicates that a good design is one that requires very little brainpower to navigate, as usually users aren’t thinking very deeply or may be distracted by other things while using this app. Overall, he felt that the app was easy to use and he really liked the font, background, and color scheme.


### User Study 3
While trying to access the home page, the user noted that the home page font was too small, so it would be helpful to make the font size of the home page bigger. Similarly, when on the home page, the user struggled to click on the “+” icon, so it would have been helpful to make the whole expandable components into buttons that can be clicked. This will let the user know they are clickable sooner than if they could only see the plus icon. Also, on the mapping task, the user struggled to leave the map after scrolling slightly down. Maybe we can make the navbar static so that it keeps its location on screen even after scrolling. The user had trouble reading some words because they blended with the background. We can fix this by enhancing contrast by changing their colors to be lighter. This user had location services disabled for their browser which lead to some glitches happening with the location dependent services like posting and finding. We should add a case for these users where they can manually set their location in the find tab.
The user overall had a decent experience with the overall layout of the app, but there were some finer adjustments that could help improve the overall user experience. They noted that most of it felt intuitive, but some word sizing, and location of buttons could definitely be improved. They said they mostly did not have to think when navigating through the app which is great. They said the app is very promising, has a good looking UI but could use further refinement. Also, adding a case for disabled location services would be very helpful. 


### Opportunities for improvement
Improve Iconography (Conceptual, Moderate): The “+” button was unclear. Make the color of the icon easier to see or make it larger.
Highlight Filtering Tools (Conceptual, Minor): Users did not discover the “sort by likes” feature. Make sorting buttons more prominent or add a brief onboarding tutorial.
Design for Users with Impaired Vision or Limited Attention (Physical, Minor): The user had trouble seeing interface changes due to poor eyesight without contacts, and was somewhat on “autopilot.” The UI does not account fully for users with mild visual impairment or those operating at reduced attention levels. A possible solution is to implement accessibility features such as adjustable contrast, larger fonts, or icon labels. Provide subtle cues or animations that clearly show state changes.




## Design Revisions


For badging, our initial outline was to have one section for the badges the user has achieved. However, we realized that the users should know their process on each of the badges, and know how many points they have left. Thus, in the profile section, the user has two options: 1. They can see what badges they have achieved, and 2. They can see the badges in process + the points they have left to achieve it.


For posting, we decided to get rid of the boosting functionality, and in replacement we added two buttons: sort by number of likes and sort by date added. This is because boosting would make the order of the posts somewhat arbitrary, since the sorting was dependent on both date added and the number of likes. We decided to simplify the functionality by adding two separate buttons.


For Mapping, we decided to get rid of the routing functionality. This routing functionality will have had to rely on a novel algorithm we do not have the time to develop. The original intention was to find “light pollution sweet spots” where users in high light pollution areas could find areas with less light pollution that were nearby with ease and get directions to said spot, however this seems very difficult to implement with the current time frame. Instead of reinventing the wheel, users can find a suitable location with less light pollution using the heatmap and just use a routing app such as google or apple maps.


For Foruming, instead of having channels listed on the side, we decided to list the forums below the create forum form. This is because the navbar is already located on the side, so the design would be a bit clunky. Instead, users can scroll through forums on the forum page, and click “enter” to enter a separate page containing the comments of that forum.


After beta testing, we identified some minor design problems, such as some buttons on the forum page not having the same styling as the other buttons, or the sidebar not filling the whole screen when the hamburger button is toggled. For the “find” page where the user can find space objects near them, we added a “guide” functionality where users can toggle a button to reveal where to look for the space objects.
