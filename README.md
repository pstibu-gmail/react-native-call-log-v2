# react-native-call-log-v2

# Call log package for react-native (Android only)

## Installation:

Run `yarn add react-native-call-log-v2`

### Android

#### React Native 0.60+

`auto links the module`

#### React Native <= 0.59

##### Auto

`react-native link react-native-call-log-v2`

#### Manual

- Edit your `android/settings.gradle` to look like this (exclude +)

```diff
+ include ':react-native-call-log-v2'
+ project(':react-native-call-log-v2').projectDir = new File(rootProject.projectDir, '../node_modules/react-native-call-log-v2/android')
```

- Edit your `android/app/build.gradle` (note: **app** folder) to look like this (exclude +)

```diff
dependencies {
+ implementation project(':react-native-call-log-v2')
}
```

- Edit your `MainApplication.java` from ( `android/app/src/main/java/...`) to look like this (exclude +)

```diff
+ import com.wscodelabs.callLogs.CallLogPackage;

@Override
    protected List<ReactPackage> getPackages() {
      return Arrays.<ReactPackage>asList(
          new MainReactPackage(),
+         new CallLogPackage()
      );
    }
```

## Usage

```javascript
import { PermissionsAndroid } from "react-native";
import CallLogs from "react-native-call-log-v2";

useEffect(() => {
  (async () => {
    try {
      const granted = await PermissionsAndroid.request(
        PermissionsAndroid.PERMISSIONS.READ_CALL_LOG,
        {
          title: "Call Log Example",
          message: "Access your call logs",
          buttonNeutral: "Ask Me Later",
          buttonNegative: "Cancel",
          buttonPositive: "OK",
        }
      );
      if (granted === PermissionsAndroid.RESULTS.GRANTED) {
        CallLogs.load(-1, filter).then((c) => console.log(c));
      } else {
        console.log("Call Log permission denied");
      }
    } catch (e) {
      console.log(e);
    }
  })();
}, []);
```

## Methods

| Methods                                     | Description                                                                                                                           |
| ------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------- |
| `load(LIMIT)`                               | `LIMIT: number` get maximum number of call logs.(use -1 for no LIMIT)                                                                 |
| `loadByType(LIMIT, TYPE)`                   | `LIMIT: number`<br> `TYPE: string` [see types](#types).                                                                               |
| `loadWithFilter(LIMIT, FILTER)`             | `LIMIT: number` (use -1 for no LIMIT)<br> `FILTER: object` [see usage here](#filter-call-logs)                                        |
| `loadByTypeWithFilter(LIMIT, TYPE, FILTER)` | `LIMIT: number` (use -1 for no LIMIT)<br> `TYPE: string` [see types](#types)<br> `FILTER: object` [see usage here](#filter-call-logs) |
| `loadAll()`                                 | get all call logs                                                                                                                     |
| `loadAllByType(TYPE)`                       | get all call logs by type.<br> `TYPE: string` [see types](#types)                                                                     |

### Types

```
OUTGOING
INCOMING
MISSED
UNKNOWN
```

### Filter call logs

```
...
/* List call logs matching the filter */
const filter = {
  minTimestamp: 1571835032,    // (Number or String) timestamp in milliseconds since UNIX epoch
                               // if this filter is set, load(limit, filter) will only return call logs with timestamp >= minTimestamp

  maxTimestamp: 1571835033,    // (Number or String) timestamp in milliseconds since UNIX epoch
                               //
                               // if this filter is set, load(limit, filter) will only return call logs with timestamp <= maxTimestamp

  phoneNumbers: '+1234567890', // (String or an Array of String)
                               // if this filter is set, load(limit, filter) will only return call logs for this/these phone numbers
}

const callLogs = await CallLogs.load(-1, filter) // applies filter with no limit (also works with a limit)
...
```

### Happy Coding!!!

## Contributing

<table>
  <tr>
    <td align="center"><a href="https://github.com/pstibu-gmail"><img src="https://avatars.githubusercontent.com/u/43640110?v=3?s=100" width="100px;" alt=""/><br /><sub><b>Tibu Padmakumar</b></sub></a><br /> <a href="https://github.com/pstibu-gmail/react-native-call-log-v2/commits?author=pstibu-gmail" title="Code">💻</a> <a href="https://github.com/pstibu-gmail/react-native-call-log-v2/commits?author=pstibu-gmail" title="Documentation">📖</a> <a href="https://github.com/pstibu-gmail/react-native-call-log-v2/pulls?q=is%3Apr+reviewed-by%3Apstibu-gmail" title="Reviewed Pull Requests">👀</a> <a href="#translation-pstibu-gmail" title="Translation">🌍</a> <a href="#talk-pstibu-gmail" title="Talks">📢</a> <a href="#question-pstibu-gmail" title="Answering Questions">💬</a> <a href="#tool-pstibu-gmail" title="Tools">🔧</a> <a href="#maintenance-pstibu-gmail" title="Maintenance">🚧</a></td>
  </tr>
 </table>
PRs are welcome
