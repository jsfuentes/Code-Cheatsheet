# Waypoint

Run a function when a waypoint is reached

```bash
yarn add react-waypoint
```

A waypoint normally fires `onEnter` and `onLeave` as you are scrolling, but it can fire because of other events too:

- When the window is resized
- When it is mounted (fires `onEnter` if it's visible on the page)
- When it is updated/re-rendered by its parent

#### Uses

- infinite scroll
- Change, add CSS on scroll 

## Example

```jsx
 import { Waypoint } from "react-waypoint";

class MenuBar extends Component {
  state = {
    scrolled: false
  };
  
   handleWaypointEnter = () => {
      this.setState({ scrolled: false });
    };

    handleWaypointLeave = () => {
      this.setState({ scrolled: true });
    };
  
  render() {
    const navClass = classNames(
        "navbar",
        { "add-nav-shadow": this.state.scrolled }
      );
    return (
      <Waypoint
        onEnter={this.handleWaypointEnter}
        onLeave={this.handleWaypointLeave}
        />
  	)
  }

```

