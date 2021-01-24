[GraphQL Voyager](https://apis.guru/graphql-voyager/)

[img](assets/images/ctf/graph.png)

```
query allTraders($before: String, $after: String, $first: Int, $last: Int, $before1: String, $after1: String, $first1: Int, $last1: Int){
    allTraders(before: $before1, after: $after1, first: $first1, last: $last1){
        pageInfo{
            hasNextPage
            hasPreviousPage
            startCursor
            endCursor
        }
        edges{
            node{
                uuid
                username
                coins(before: $before, after: $after, first: $first, last: $last){
                    pageInfo{
                        hasNextPage
                        hasPreviousPage
                        startCursor
                        endCursor
                    }
                    edges{
                        cursor
                    }
                }
                id
            }
            cursor
        }
    }
}
``
