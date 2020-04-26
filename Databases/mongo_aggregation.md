# Mongo Aggregation

Instead of SQL, use the **pipeline** to create complex queries. MongoDB compass has a great editor for this that creates the structure and shows you the results at each step.

- $lookup - basically like an SQL join that takes all the matches from the foreign table and puts it in an array named as
- $unwind - takes an array path and makes a seperate entry for each array element with its parent {x: 1, y: [1,2]} => {x: 1, y: 1}, {x: 1, y: 2}
- $replaceRoot - allows you to create a new doc and clean up grabbing fields from nested and such
- $group - basically a group by
  - $sum - put sum: 1 to just do a count  
  - $push - to create array of each value

## Example

```json
[{
    $lookup: {
        from: 'companies',
        localField: 'user.company_id',
        foreignField: '_id',
        as: 'company'
    }
}, {
    $unwind: {
        path: "$company",
        preserveNullAndEmptyArrays: false
    }
}, {
    $replaceRoot: {
        newRoot: {
            user: "$user.name",
            email: "$user.email",
            user_pic: "$user.pic",
            url: "$video.s3_url",
            folder_id: "$_id",
            date_created: "$date_created",
            company_name: "$company.name",
            company_logo: "$company.logo_url"
        }
    }
}, {
    $group: {
        _id: "$email",
        count: {
            $sum: 1
        },
        videos: {
            $push: {
                date_created: "$date_created",
                url: "$url",
                folder_id: "$folder_id"
            }
        }
    }
}]
```

