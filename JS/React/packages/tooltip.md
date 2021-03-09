# React-Tooltip

```bash
yarn add react-tooltip
```

## Usage

Add data-for and id's so can have multiple

```
import ReactTooltip from "react-tooltip";

            <div>
              <a
                data-for={id}
                data-tip="Event Organizer"
                // style={{ padding: "0.15rem" }}
                className="cursor-pointer text-sm absolute bottom-0 -left-2  w-5 h-5 branded-lightest shadow-xs rounded-full flex justify-center items-center"
              >
                <i className="bx bxs-star branded-darker-color"></i>
              </a>
              <ReactTooltip
                id={id}
                type="dark"
                effect="solid"
                className="my-tooltip-dark"
                place="left"
                arrowColor="#323232"
              />
            </div>
```

