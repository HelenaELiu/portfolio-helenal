---
title: Assignment 4
layout: doc
---

# Assignment 4: Backend Design & Implementation (Alpha)

---

Abstract Data Models:
1. Concept Name: Events
    - Purpose: Users can create an event to inform others about upcoming classes, workshops, etc.
    - Operational Principle: Users input certain required information about their event (name, time, location, etc.) and the event is created on the events page for other users to see until the event has passed
    - State: 
        - name: one String
        - time: one Date
        - location: one String
        - price: one Number
        - description: one String
        - choreographers: set String
        - genres: set String
        - props: set String
        - attendees: set String
    - Actions:
        - createEvent (name: String, time: Date, location: String, choreographers: set String, genres: set String, props: set String, price: Number, description: String)
        - deleteEvent (event: Event)
        - updateName (event: Event, name: String)
        - updateTime (event: Event, time: Date)
        - updateLocation (event: Event, location: String)
        - updatePrice (event: Event, price: Number)
        - updateDescription (event: Event, description: String)
        - addChoreog (event: Event, choreographer: String)
        - deleteChoreog (event: Event, choreographer: String)
        - addGenre (event: Event, genre: String)
        - deleteGenre (event: Event, genre: String)
        - addProp (event: Event, prop: String)
        - deleteProp (event: Event, prop: String)
        - addAttendee(event: Event, attendee: String)
        - deleteAttendee(event: Event, attendee: String)
2. Concept Name: Video
    - Purpose: Users can upload videos showcasing their dance ability
    - Operational Principle: Users upload a video (maximum 1 minute) that displays their dancing, and the video is displayed on their profile. This video appears in a grid of videos on the profile and can be tapped on to be watched
    - State:
        - const data: array Number
        - const description: one String
        - const id: one String
    - Actions:
        - createVideo (data: array Number, description: String)
        - watchVideo (video: Video)
        - deleteVideo (video: Video)
3. Concept Name: Organizations
    - Purpose: Users can join organizations to find other people that attend the same dance studio or are part of the same dance team
    - Operational Principle: Users create an organization and other users can join. Public organizations allow all users to join, while private organizations have someone currently a part of the organization approve new members. Organizations can be searched for on the organizations page
    - State: 
        - name: one String
        - description: one String
        - members: set User
        - private: one Boolean //false is public, true is private
    - Actions:
        - createOrg (name: String, description: String, creator: User, private: Boolean) //creator gets added to set of members
        - deleteOrg (org: Organization)
        - updateName (org: Organization, name: String)
        - updateDescription (org: Organization, description: String)
        - addMember (org: Organization, member: User)
        - deleteMember (org: Organization, member: User)
        - makePublic(org: Organization) 
        - makePrivate(org: Organization)  
4. Concept Name: Map
    - Purpose: Users can scroll through a map to find locations of events relative to their current location
    - Operational Principle: Users open the map page and are prompted to input some values into filters (date, location, and genre), none of which they are required to fill out. Then, based on these filters, pins are dropped on the map showing events that satisfy the constraints described by the filters, as well as a differently colored pin indicating current location. These pins can be tapped on to bring up a small window showing what event they correspond to, and tapping away from these pins makes the window disappear.
    - State:
        - events: set Event
        - dateFilter: set Date
        - currentCoord: Coord //gps coordinates, not address
        - locationRadius: Int
        - genreFilter: set String
    - Actions:
        - scroll (map: Map)
        - dropPins (map: Map, dateFilter: set Date, currentCoord: Coord, locationRadius: Int, genreFilter: set String)
        - tapPin (map: Map, event: Event)
        - untapPin (map: Map, event: Event)
5. Concept Name: Invites
    - Purpose: Users can invite other users to events to spread the word.
    - Operational Principle: If a user wants to send an invite to another user, they tap on the invite button and search for the user that they want to send the invite to. When a user receives an invite, they can choose to respond “yes”, “no”, or “maybe”, or leave it unanswered.
    - State: 
        - event: one Event
        - from: one User
        - to: one User
        - status: one String //can be “rejected”, “accepted”, or “pending”
    - Actions:
        - sendInvite (event: Event, from: User, to: User) //default status is pending
        - acceptInvite (invite: Invite)
        - rejectInvite (invite: Invite)
        - removeInvite (invite: Invite)

---

Backend code repository: https://github.com/HelenaELiu/backend-starter
Vercel Deployment: https://backend-starter-377zmfub5-helena-lius-projects.vercel.app