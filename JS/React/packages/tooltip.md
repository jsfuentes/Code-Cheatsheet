# React-Tooltip

```bash
yarn add react-tooltip
```

## Usage

somewhere in app

```react
import 'react-tooltip/dist/react-tooltip.css'
```

Add data-for and id's so can have multiple using same tooltip

```jsx
import { Tooltip } from 'react-tooltip'

<div className="font-medium flex flex-row items-center">
  <div className="text-2xl">
    {" "}
    Current Portfolio Value: ${totalRewardDynamic}
  </div>
  <i
    className="bx bx-info-circle ml-1"
    data-tooltip-id="dashboard-tooltip"
    data-tooltip-content="Current market value of the Bitcoin earned shown in $"
    data-tooltip-place="top"
  />
</div>

<div className="font-medium flex flex-row items-center">
  <div className="text-2xl">
    Total Bitcoin: {totalBitcoinReward} BTC
  </div>
  <i
    className="bx bx-info-circle ml-1"
    data-tooltip-id="dashboard-tooltip"
    data-tooltip-content="Bitcoin earned shown in Satoshis"
    data-tooltip-place="top"
  />
</div>

<Tooltip id="dashboard-tooltip" delayHide={0} />
```

Apparently you can just add a Tooltip anywhere without an id and then add data-tip
