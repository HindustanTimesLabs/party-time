<!-- Generated by documentation.js. Update this documentation by updating the source code. -->

### Table of Contents

-   [getType](#gettype)
-   [getInfo](#getinfo)
-   [convert](#convert)

## getType

[build/party-time.js:4195-4204](https://github.com/HarryStevens/party-time/blob/570c72165e83d833d77884a6f32d6bc735324c89/build/party-time.js#L4195-L4204 "Source code on GitHub")

Guesses whether the party string entered is an abbreviation or the full name.

**Parameters**

-   `party` **[string](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String)** The party, either a full name or an abbrevation.

Returns **[string](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String)** Returns "abbr" or "name".

## getInfo

[build/party-time.js:4245-4262](https://github.com/HarryStevens/party-time/blob/570c72165e83d833d77884a6f32d6bc735324c89/build/party-time.js#L4245-L4262 "Source code on GitHub")

Gets information about the party. If you do not specify a type in the second argument, it will guess the type.

**Parameters**

-   `party` **[string](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String)** The party, either a full name or an abbrevation, to get information about.
-   `type` **[string](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String)** A type, which can be either "abbr" or "name". This argument is optional. `party-time` usually can determine the type by itself, but you can declare it explicitly, just in case. (optional, default `null`)

**Examples**

```javascript
pt.getInfo("BJP");
//{   
//  name: "Bharatiya Janata Party",
//  abbr: "BJP",
//  founded: 1980,
//  type: "national",
//  location: "India",
//  symbol: "Lotus" 
//}

pt.getInfo("Indian National Congress");
//{ 
//  name: "Indian National Congress",
//  abbr: "INC",
//  founded: 1885,
//  type: "national",
//  location: "India",
//  symbol: "Hand"
//}

pt.getInfo("cpm");
//{ 
//  name: "Communist Party of India (Marxist)",
//  abbr: "CPI(M)",
//  founded: 1964,
//  type: "national",
//  location: "India",
//  symbol: "Hammer sickle and star",
//  variations: { abbr: [ "CPM" ] } 
//}

pt.getInfo("Not a real party") // { name: 'Not a real party', warning: 'No match in library' }
```

Returns **[object](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object)** An object with information about the party. If the party entered is not found in the library, returns an object containing the party name and a warning.

## convert

[build/party-time.js:4283-4316](https://github.com/HarryStevens/party-time/blob/570c72165e83d833d77884a6f32d6bc735324c89/build/party-time.js#L4283-L4316 "Source code on GitHub")

Converts a party abbreviation to its full name or vice versa. If the party entered is not found in the library, returns the party entered.

**Parameters**

-   `party` **[string](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String)** The party, either a full name or an abbrevation, to convert.
-   `options` **[object](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object)** An object specifying options for the conversion. (optional, default `{greedy:TRUE}`)
    -   `options.greedy` **[boolean](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Boolean)** If `true`, the function does the conversion automatically and returns a string. If there is no match in the library, it will return the original string. If `false`, the function returns an object with the properties `abbr`, `name` and, when applicable, `variations`. (optional, default `TRUE`)
    -   `options.type` **[string](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String)** By default, the function will guess the type of the party string by matching it against the party names and abbreviations in the library. You can override this behavior and explicitly specify the type of party string by passing `"abbr"` or `"name"`. (optional, default `null`)

**Examples**

```javascript
pt.convert("BJP"); // "Bharatiya Janata Party"
pt.convert("BJP", { greedy: false }); // { abbr: "BJP", name: "Bharatiya Janata Party" }
pt.convert("BJP", { greedy: true }); // "Bharatiya Janata Party"
pt.convert("bjp"); // "Bharatiya Janata Party"
pt.convert("cpm", { greedy: false }); // { abbr: "CPI(M)", name: "Communist Party of India (Marxist)", variations: { abbr: ["CPM"] } }
pt.convert("Indian National Congress"); // "INC"
pt.convert("Not a real party"); // "Not a real party"
pt.convert("NARP"); // "NARP"
pt.convert("narp", { type: "abbr" }); // "narp"
pt.convert("narp", { greedy: false, type: "name" }); // { name: "narp", warning: "No match in libary" }
```

Returns **([string](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String) \| [object](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object))** A string with the converted party or, if the conversion is not set to greedy, an object with information about the party.
