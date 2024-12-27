# React-Table

```bash
yarn add react-table
```

## Usage

Table.js

```jsx
import React from "react";
import { useTable } from "react-table";
const debug = require("debug")("app:Table");

export default function Table({ columns, data }) {
  // Use the state and functions returned from useTable to build your UI
  const {
    getTableProps,
    getTableBodyProps,
    headerGroups,
    rows,
    prepareRow,
  } = useTable({
    columns,
    data,
  });

  debug("getTableBodyProps", getTableBodyProps());

  // Render the UI for your table
  return (
    <table
      {...getTableProps()}
      className="w-full bg-pureWhite border border-gray-200 border-1 hover:bg-gray-50"
    >
      <thead className="p-4 font-bold border border-gray-200 border-b">
        {headerGroups.map((headerGroup) => (
          <tr {...headerGroup.getHeaderGroupProps()}>
            {headerGroup.headers.map((column) => (
              <th {...column.getHeaderProps()} className="p-4 m-0">
                {column.render("Header")}
              </th>
            ))}
          </tr>
        ))}
      </thead>
      <tbody {...getTableBodyProps()} className="p-4 cursor-pointer">
        {rows.map((row, i) => {
          prepareRow(row);
          return (
            <tr
              {...row.getRowProps()}
              className="border border-gray-200 border-b"
            >
              {row.cells.map((cell) => {
                return (
                  <td {...cell.getCellProps()} className="p-4 m-0">
                    {cell.render("Cell")}
                  </td>
                );
              })}
            </tr>
          );
        })}
      </tbody>
    </table>
  );
}
```

App.js

```jsx
import React, { useState, useEffect, useMemo } from "react";
import Table from "src/components/Table";
const debug = require("debug")("app:Dashboard");

export default function Dashboard(props) {
  const [events, setEvents] = useState(null);
  const columns = useMemo(
    () => [
      {
        Header: "Title/Date",
        accessor: "title",
      },
      {
        Header: "Start Time",
        accessor: "start_time",
      },
      {
        Header: "Visitors",
        accessor: "view",
      },
      {
        Header: "RSVP",
        accessor: "rsvp",
      },
      {
        Header: "Attended",
        accessor: "join",
      },
    ],
    []
  );

  function renderEventList() {
    return (

    );
  }

  return (
    <div>
      <Navbar>
        <UserDropdown />
      </Navbar>
      <div className="container mx-auto w-full mt-8 sm:mt-16 md:max-w-3xl lg:max-w-4xl mb-20 ">
        <div className="flex justify-between items-center">
          <h1 className="text-2xl sm:text-3xl font-medium">My Events</h1>
          <Button
            iconLeft
            icon="bx-plus"
            size="medium"
            onClick={() => goToBaseEvent()}
          >
            Create Event
          </Button>
        </div>
        {events === null ? (
          <div> Loading... </div>
        ) : events.length === 0 ? (
          <div>0 Events here</div>
        ) : (
          <div className="w-full mt-10 bg-pureWhite border border-gray-200">
            <Table columns={columns} data={events} />
          </div>
        )}
      </div>
    </div>
  );
}

```

