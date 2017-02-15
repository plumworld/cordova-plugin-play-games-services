cordova-plugin-play-games-services
==================================

Cordova Plugin For Google Play Games Services (Fork of [artberri/cordova-google-play-game](https://github.com/artberri/cordova-google-play-game))

Modified to add exception handling.

### Before you start

Understand about **Leaderboard** and **Achievement**. Setting up your game in Google Play Developer Console https://developers.google.com/games/services/android/quickstart

## Install

Cordova >= 5.0.0

```
cordova plugin add cordova-plugin-play-games-services --variable APP_ID=you_app_id_here
```

Cordova < 5.0.0

```
cordova plugin add https://github.com/artberri/cordova-plugin-play-games-services.git --variable APP_ID=you_app_id_here
```

## Usage

### Authentication

#### Sign in
You should do this as soon as your `deviceready` event has been fired. The plugin handles the various auth scenarios for you.

```
window.plugins.playGamesServices.auth();
```

#### Sign out
You should provde the option for users to sign out

```
window.plugins.playGamesServices.signout();
```

#### Auth status
To check if the user is already logged in (eg. to determine weather to show the Log In or Log Out button), use the following

```
window.plugins.playGamesServices.isSignedIn(function (result) {
	// ‘result’ is a JSON object with a single boolean property of ‘isSignedIn’
	// {
	// 		“isSignedIn” : true
	// }

	console.log(“Do something with result.isSignedIn”);
});
```

#### Player Information
Fetch the currently authenticated player's data.

```
window.plugins.playGamesServices.showPlayer(function (playerData) {
	...
	console.log(“Authenticated as ”+playerData['displayName']);
});
```


### Leaderboards

#### Submit Score

Ensure you have had a successful callback from `window.plugins.playGamesServices.auth()` first before attempting to submit a score. You should also have set up your leaderboard(s) in Google Play Game Console and use the leaderboard identifier assigned there as the `leaderboardId`.

```
var data = {
    score: 10,
    leaderboardId: "board1"
};
window.plugins.playGamesServices.submitScore(data);
```

#### Show all leaderboards

Launches the native Play Games leaderboard view controller to show all the leaderboards.

```
window.plugins.playGamesServices.showAllLeaderboards();
```

#### Show specific leaderboard

Launches directly into the specified leaderboard:

```
var data = {
	leaderboardId: "board1"
};
window.plugins.playGamesServices.showLeaderboard(leaderboardId);
```

### Achievements
#### Unlock achievement

Unlocks the specified achievement:

```
var data = {
	achievementId: "achievementId1"
};

window.plugins.playGamesServices.unlockAchievement(data);
```

#### Increment achievement

Increments the specified incremental achievement by the provided numSteps:

```
var data = {
	achievementId: "achievementId1",
	numSteps: 1
};

window.plugins.playGamesServices.incrementAchievement(data);
```

#### Show achievements

Launches the native Play Games achievements view controller to show the user’s achievements.

```
window.plugins.playGamesServices.showAchievements();
```

### Other

#### Success/Failure callbacks

For all methods, you can optionally provide custom success/failure callbacks.

For example:

```
var successfullyLoggedIn = function () { ... };
var failedToLogin = function () { ... };
window.plugins.playGamesServices.auth(successfullyLoggedIn, failedToLogin);

var data = { ... };
var successfullySubmittedScore  = function () { ... };
var failedToSubmitScore  = function () { ... };
window.plugins.playGamesServices.submitScore(data, successfullySubmittedScore, failedToSubmitScore);
```

## Platform

Currently, only Android is supported


## License

[MIT License](http://ilee.mit-license.org)
