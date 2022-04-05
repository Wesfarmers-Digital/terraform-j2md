terraform-j2md
===
Output human-readable markdown texts from Terraform plan JSON output.

## Synopsis
Terraform can report plan to [machine-readable JSON file](https://www.terraform.io/language/syntax/json).
_terraform-j2md_ is simple conversion tool, from Terraform JSON to Markdown texts.

Output texts may be useful as pull-request comments, and so on.

## How to use

### Installation
(TBD)

### Usage
_terraform-j2md_ reads only standard input, write only standard output.
```
terraform-j2md < [input file] > [output file]
```

### Example
````sh
$ terraform init
$ terraform plan -out plan.tfplan

Terraform used the selected providers to generate the following execution plan. Resource actions are indicated with the following symbols:
  + create

Terraform will perform the following actions:

  # null_resource.foo will be created
  + resource "null_resource" "foo" {
      + id = (known after apply)
    }

Plan: 1 to add, 0 to change, 0 to destroy.

─────────────────────────────────────────────────────────────────────

Saved the plan to: plan.tfplan

To perform exactly these actions, run the following command to apply:
    terraform apply "plan.tfplan"

$ terraform show -json plan.tfplan | terraform-j2md
### 1 to add, 0 to change, 0 to destroy, 0 to replace.
- add
    - null_resource.foo
<details><summary>Change details</summary>

```diff
# null_resource.foo will be created
@@ -1 +1,3 @@
-null
+{
+  "triggers": null
+}
```

</details>

````

## How to test/build
### Test
```
go test ./...
```

### Build
```
go build -o terraform-j2md main.go
```
