# Room category ImageIds deprecation
`ImageIds` field of [room category](../operations.md#room-category) object is deprecated and will be removed from the responses of [configuration/get](../operations.md#get-configuration) and [hotels/get](../operations.md#get-hotels). It is replaced by [Category image assignment](../operations.md#category-image-assignment) on [configuration/get](../operations.md#get-configuration) endpoint. This will mainly allow you to get more information for that image, such is `Ordering` field that can be used for displaying the images in specific order. 

## Response diff

```diff
{
    ...
    "Configurations": [
        {
            ...
            "Enterprise": {
                ...
                "Categories": [
                    {
                        ...
-                       "ImageIds": ["f987a97c-5049-44ca-9933-5b657e5263e2"],
                    }
                ],
+               "CategoryImageAssignments": [
+                   {
+                     "Id": "69832f4b-4b47-4d32-9b89-ac0600de0cd6",
+                     "CategoryId": "295d96e7-8501-4cbd-b78d-8bf590bf6db9",
+                     "ImageId": "f987a97c-5049-44ca-9933-5b657e5263e2",
+                     "Ordering": 2
+                   }
+               ]
            }
        }
    ]
}
```
