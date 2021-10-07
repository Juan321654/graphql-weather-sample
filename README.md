Just a sample on how to use graphql client

```jsx
import React, { useState, useEffect } from "react";
import { useMutation } from "@apollo/client";
import Card from "react-bootstrap/Card";
import UPDATE_PRODUCTS from "../../helpers/UPDATE_PRODUCTS";
import Button from "react-bootstrap/Button";

const UpdateProducts = () => {
  const [updateState, setUpdateState] = useState(false);
  const [setProductData, { error: productError, data: mutationProductData }] =
    useMutation(UPDATE_PRODUCTS());

    // import { gql } from "@apollo/client";

    // export default function CREATE_PRODUCT() {
    //   return gql`
    //     mutation productUpdate($input: ProductInput!) {
    //       productUpdate(input: $input) {
    //         product {
    //           id
    //           title
    //           handle
    //         }
    //       }
    //     }
    //   `;
    // }

  useEffect(() => {
    if (updateState) {
      setProductData({
        variables: {
          input: {
            id: "gid://shopify/Product/7007884837022",
            title: "updated from react",
            variants: {
              compareAtPrice: 599.22,
              price: 399.99,
              inventoryItem: {
                cost: "89.99",
              },
            },
          },
        },
      });
    }
    setTimeout(() => {
      setUpdateState(false);
    }, 2000);
  }, [updateState]);

  // axios call should return this
  // return setProductData({
  //   variables: {
  //     title: "something",
  //   },
  // });

  // {
  //   "input": {
  //     "id": "gid://shopify/Product/7007884837022",
  //     "title": "new title form imnsonia",
  //     "variants": {
  //       "compareAtPrice": 100.57,
  //       "price": 999.9,
  //       "inventoryItem": {
  //         "cost": "29.99"
  //       }
  //     }
  //   }
  // }

  return (
    <Card
      style={{ borderColor: "darkseagreen" }}
      className="card-border-width4 card-max-width card-margin card-shadow"
    >
      <Card.Body>
        <Card.Title>Update products</Card.Title>
        <Button onClick={() => setUpdateState(true)}>update</Button>
      </Card.Body>
    </Card>
  );
};

export default UpdateProducts;

```