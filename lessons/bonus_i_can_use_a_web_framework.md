# Bonus: I Can Use a Web Framework

## React - An Overview

### Reference

  - https://reactjs.org/docs/create-a-new-react-app.html

## Setup

### Open Command Prompt

Open a command prompt and go to the 'Desktop' subdirectory
by entering the `cd Desktop` command.

### Create Project

From the command line, enter the following command.
```
npx create-react-app my-app
```

### Open IDE

Open `VS Code` and do the following.
  - From the menu, select `File` then `Open`
  - Select the `my-app` directory from the `Desktop` directory
  - Click the `Open` button

### Open Terminal within IDE

It's possible to open a command line pane within `VS Code`
so that it doesn't need to be opened up separately!

From within `VS Code` do the following.
  - From the menu, select `Terminal` then `New Terminal`
  - A terminal pane should appear
    - It's current directory is the base directory of the project (`~/Desktop/my-app`)
    - Having a separate terminal window is no longer needed!

### Download Libraries

The `dependencies` entries in the `package.json` file lists all
of the libraries this project depends on. Those libraries
get downloaded when the `npx create-react-app my-app`
into the `node_modules` directory which is the standard directory
where libraries get downloaded.

The `npm install` command is used to download libraries
and update what's downloaded into the `node_modules` directory
if the `dependencies` entries change. Run the `npm install` command
in the terminal pane now to get better familiarity with that command.

### Run Project Locally

In the terminal pane, run `npm start` to start the server locally.
Doing so should automatically open a browser to URL
`http://localhost:3000/` but if not open a browser and to there.
It will show a simple page with atom icon and `Learn React` text.

#### Stop the Local Server

To stop the server, select the terminal pane, then hold down
the `Control` key then press the `c` key (this combination
is known as the 'hot key' `Control-C`).

#### How `npm start` Works

Under the `scripts` section in the `package.json` file,
the `start` entry corresponds to command `react-scripts start`
which is the command that can be run on the command line.

The `node_modules/react-scripts/package.json` file contains
this entry.

```
  "bin": {
    "react-scripts": "./bin/react-scripts.js"
  },
```

When downloading the `react-scripts` module, `npm` will take
the `node_modules/react-scripts/bin/react-scripts.js` file
and copy it to the `node_modules/.bin/react-scripts` file.
Files in the `node_modules/.bin` directory are executed if they
are found in the `scripts` section of the `package.json` file
of the project.

Reference - https://docs.npmjs.com/cli/v9/configuring-npm/package-json#bin

#### How React Runs for This Case

`public/index.html` is the page that gets loaded when a browser
goes to `http://localhost:3000/` . The `public` directory is
the directory that the local web server will serve a file
from when it receives a request. `index.html` is the file
that gets served when the URL doesn't include a specific file.

Enter `http://localhost:3000/robots.txt` into a browser
while the server is running and it will respond with the following.

```
# https://www.robotstxt.org/robotstxt.html
User-agent: *
Disallow:
```

That's the same contents as the content found
at `public/robots.txt` .

##### Specific Mechanism

The source for the page rendered by `http://localhost:3000/`
includes the following statement.

```
 <script defer src="/static/js/bundle.js"></script></head>
```

Unlike other lines in `public/index.html` , this statement gets inserted
by the local React web server and the `/static/js/bundle.js` file
is the result of React compiling the `src/index.js` file
and all of the files it depends on.

The `src/index.js` file contains the following segment.

```
const root = ReactDOM.createRoot(document.getElementById('root'));
root.render(
  <React.StrictMode>
    <App />
  </React.StrictMode>
);
```

Likewise, the `public/index.html` contains the following HTML tag.
```
    <div id="root"></div>
```

The `document.getElementById('root')` statement identifies this HTML tag
and the 'App' tag (however React renders it as HTML tags) is placed
as the content within this tag.

The 'App' tag is referenced by this statement in the `src/index.js` file.

```
import App from './App';
```

This `import` statement references the file `src/App.js` which defines
the 'App' tag as follows.

```
function App() {
  return (
    <div className="App">
...
    </div>
  );
}
```

There are two important facts about this `src/App.js` file.

1) The 'App' function contains HTML notation
which isn't normally allowed in JavaScript.
2) 'App' isn't an HTML tag but instead is a JavaScript function.

These two 'anamolies' are _foundational_ to React.

1) Developers can create functions which execute when written
as HTML tags (like '<App />').
2) Those functions can include HTML tags which get included in the DOM.

### Run Unit Tests

It's common practice for professional developers to write code to test
select segments of code. This type of code is called `unit tests`
and the `src/App.test.js` file contains the following test.

```
test('renders learn react link', () => {
  render(<App />);
  const linkElement = screen.getByText(/learn react/i);
  expect(linkElement).toBeInTheDocument();
});
```

In this test, the 'App' tag is rendered (in memory, not in a browser)
and then the test checks whether text (represented by regular expression
`/learn react/i`) is found in the rendered output.

Run the unit tests (actually there's just one) of this project
with the `npm test` command in the terminal pane then press the 'a' key.

Change `/learn react/i` to `/unlearn react/i` and save
the `src/App.test.js` file. The unit test will automatically rerun and fail
because 'unlearn' won't be found in the rendered output. Revert and save
the change and the unit test will now pass. Press 'q' in the terminal pane
to stop the unit-test running program.
