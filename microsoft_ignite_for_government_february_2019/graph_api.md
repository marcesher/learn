# MS Graph API

tons of stuff available in the API... users, groups, excel, onedrive, outlook, contacts, sharepoint, delta query, webhooks


## Examples of apps using the API

  - Delve: people-based search
  - Sharepoint home

note: the full sharepoint search engine isn't yet available in the API; theyre working on it

  - Microsoft Word - Tap
    - office add-in, basically a web page hosted inside of word to try to surface relevant stuff you've worked on recently; uses graph to pull in those things


all of this discovery / aggregation stuff is controllable by administrators

"people cards and profiles"

- all the info that you see in the people view comes from ms graph API

##Working with MS Graph

graph.microsoft.com/{version}

versions: /v1.0, /beta

/beta: no guarantee it'll make it into 1.0; he's seen APIs in /beta for 1.5 years and not make it

CRUD = http verbs: post, get, patch, delete

recommendation: sign up for the developer program; this gets you your own personal tenancy, for practicing

dev.office.com/

resources: /users, /groups, /sites, /drives, /devices, etc etc

note that they've tried to not be product-specific here; eg both sharepoint and onedrive file-related stuff available in /drives

- member from collection = /users/mikeam
- property: /users/mikeam/department
- resources via navigations: /users/mikeam/events
- query parameters: /users/mikeam/events?$top=5 and a handful of these kinds of things for formatting, controlling, paging

key architectural thing to note: much of what's represented in Graph is based on "Groups"

"/me" to get your own stuff, eg /me/insights, /me/drive/recent, /me/findMeetingTimes

/people: pulls together the people you interact with across all (most?) of the products... this is slick. Orders by most interacted with / relevance



## Graph explorer

docs, reference: here's where to see all the things you can do

you can use the graph explorer without authenticating to do GET requests; need to sign in to do all requests. Use the picker on the left hand side to change the verb (to patch, eg) and then run the update

He shows a cool example of using the graph explorer to easily create a calendar invite, and then it shows up on his calendar seamlessly


SDKs, samples, and tooling -- available for lots of languages, along with VSCode integration

he's in demo mode now for using vs code to use an SDK to get started building an application that uses the graph api

it's a react app; "I'm just gonna paste in some code here" and then pastes a buttload of code. haha. nice.

use a library called hello.js which is a library for authenticating against oauth based sources, such as graph / azure AD; this sets a token that must be used on all graph API requests

he has examples for using that token in some requests... axios.post( {headers: {Authorization: 'Bearer ${token}' }}... )

the next thing i'm gonna do is i'm gonna go just fix something.... then goes and fiddles with some other pre-built code


You need to register your app to get an application identifier... apps.dev.microsoft.com; this gets you an app ID, and then you can configure the app... what URLs that can use it, etc etc, add the permissions it's allowed to have against the graph API

there's also "microsoft authentication library" MSAL for authentication


permission type: "application" for use with service / daemon apps; this is a heavy hammer, only administrators can assign this type of permission


Track changes: webhooks + delta query

- as things change, events get fired. webhook notifications can be used as triggers to make delta query calls, which you can put in a queue for later processing if you wish. delta query basically lets you see "what's changed"

he shows a slick app he built that monitors a sharepoint folder, and when audio files are uploaded, it sends them to bing to have them transcribed, then it sends the transcription to a site or file or some shit

Microsoft Graph Data Connect -- kind of a data pipeline; built-in tool to push data to azure, keeps data within compliance boundaries



