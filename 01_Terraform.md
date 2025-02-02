# Terraform Folder Structure and Variable Handling

## 1. Recommended Terraform Folder Structure
A well-structured Terraform project should have the following key files:

1. **Main Configuration File (`main.tf`)**  
   - Contains the primary infrastructure definitions, including AWS resources such as EC2 instances, VPCs, and security groups.
   
2. **Variables Definition File (`variables.tf`)**  
   - Defines all variables that will be used in the Terraform configuration. It does not assign values but only declares them.

3. **Variable Values File (`terraform.tfvars`)**  
   - Provides actual values for the variables defined in `variables.tf`. It helps in separating configuration logic from data.

### Example Structure
```sh
.
├── main.tf            # Main Terraform configuration file
├── variables.tf       # Defines the variables
└── terraform.tfvars   # Assigns values to the variables
```

---

## 2. Explanation of Terraform Files
### a. `main.tf` (Main Configuration File)
This file contains the resource configurations. For example:

```hcl
resource "aws_vpc_security_group_ingress_rule" "allow_tls_ipv4" {
  security_group_id = aws_security_group.allow_tls.id
  cidr_ipv4         = var.vpn_ip
  from_port         = var.app_port
  ip_protocol       = "tcp"
  to_port           = var.app_port
}
```
- `cidr_ipv4 = var.vpn_ip`: Uses a variable for the IP range.
- `from_port = var.app_port`: Uses a variable for the port.

### b. `variables.tf` (Declaring Variables)
This file declares the variables used in `main.tf`:

```hcl
variable "vpn_ip" {}
variable "app_port" {}
```
- These variables are placeholders and do not have values yet.

### c. `terraform.tfvars` (Assigning Values)
This file assigns values to the variables declared in `variables.tf`:

```hcl
vpn_ip   = "101.0.62.210/32"
app_port = "8080"
```
- Now, `vpn_ip` will be `"101.0.62.210/32"` and `app_port` will be `8080`.

### How Terraform Decides Variable Values?
1. If a variable is defined in `terraform.tfvars`, it takes precedence.
2. If not found in `terraform.tfvars`, Terraform checks environment variables.
3. If not found in environment variables, it uses the default value (if any) from `variables.tf`.
4. If no default value is found, Terraform will prompt the user for input.

---

## 3. Terraform Configuration for Multiple Environments
Organizations often have multiple environments like **Development (Dev), Staging, and Production (Prod)**. Terraform allows using separate `*.tfvars` files for different environments.

### Example:
#### `main.tf`
```hcl
resource "aws_instance" "web" {
  ami           = "ami-1234"
  instance_type = var.instance_type
}
```
#### `variables.tf`
```hcl
variable "instance_type" {}
```
#### Different `*.tfvars` files for environments
**Dev Environment (`dev.tfvars`)**
```hcl
vpn_ip        = "52.0.62.30/32"
app_port      = "8080"
instance_type = "t2.micro"
```
**Prod Environment (`prod.tfvars`)**
```hcl
vpn_ip        = "101.0.62.210/32"
app_port      = "8080"
instance_type = "m5.large"
```
### Using Terraform for a Specific Environment
To apply Terraform for a specific environment, use:

```sh
terraform apply -var-file="dev.tfvars"
```
or
```sh
terraform apply -var-file="prod.tfvars"
```
- This helps manage different environments efficiently.

---

## Summary
- **`main.tf`** → Contains the infrastructure definition.
- **`variables.tf`** → Declares variables (no values assigned).
- **`terraform.tfvars`** → Assigns values to variables.
- **Default Behavior:** Terraform automatically loads terraform.tfvars and terraform.tfvars.json without requiring -var-file.
- **Explicit Declaration:** When using a different name (e.g., prod.tfvars, dev.tfvars), you must use -var-file to let Terraform know which file to use.
- Multiple `*.tfvars` files help manage different environments.

This structure keeps Terraform code clean, reusable, and easy to manage across environments.

---

# **Terraform Variable Definition Precedence**

Terraform loads variables in a specific order, where later sources take precedence over earlier ones. This means that if the same variable is defined in multiple places, Terraform will use the value from the highest-precedence source.

---

## **Order of Variable Precedence**

1. **Environment Variables**  
   - Terraform allows variables to be set using environment variables prefixed with `TF_VAR_`.  
   - Example:  
     ```sh
     export TF_VAR_instance_type="t2.large"
     terraform apply
     ```
   - Here, Terraform will use `t2.large` for the `instance_type` variable.

2. **terraform.tfvars File (if present)**  
   - If a file named `terraform.tfvars` exists, Terraform automatically loads it.  
   - Example `terraform.tfvars`:
     ```hcl
     instance_type = "t2.medium"
     ```
   - If an environment variable is also set, this file **overrides** it.

3. **terraform.tfvars.json File (if present)**  
   - Similar to `terraform.tfvars`, but in JSON format.  
   - Example `terraform.tfvars.json`:
     ```json
     {
       "instance_type": "t2.small"
     }
     ```
   - This takes precedence over the previous `.tfvars` file.

4. **Any `.auto.tfvars` or `.auto.tfvars.json` Files**  
   - Terraform automatically loads files ending in `.auto.tfvars` or `.auto.tfvars.json`.  
   - If multiple `.auto.tfvars` files exist, they are processed in **lexical order**.
   - Example:
     ```
     01-default.auto.tfvars
     02-production.auto.tfvars
     ```
   - If both files define `instance_type`, the value from `02-production.auto.tfvars` is used.

5. **Command-Line Options (`-var` and `-var-file`)**  
   - These have the **highest precedence** and override all other sources.  
   - Example:
     ```sh
     terraform apply -var "instance_type=t2.micro"
     ```
   - This will override any value defined in `.tfvars`, `.auto.tfvars`, or environment variables.

   - If using a non-standard variable file, use:
     ```sh
     terraform apply -var-file="custom.tfvars"
     ```
   - This explicitly loads variables from `custom.tfvars`.

---

## **Example Scenario: Resolving Conflicts**

Suppose we define `instance_type` in multiple places:

### **Environment Variable**
```sh
export TF_VAR_instance_type="t2.large"
```

### **terraform.tfvars**
```hcl
instance_type = "t2.medium"
```

### **terraform.tfvars.json**
```json
{
  "instance_type": "t2.small"
}
```

### **01-default.auto.tfvars**
```hcl
instance_type = "t2.micro"
```

### **02-production.auto.tfvars**
```hcl
instance_type = "t2.nano"
```

### **Command Line**
```sh
terraform apply -var "instance_type=t3.large"
```

### **Final Value Used by Terraform?**
1. **Command-line value (`t3.large`) wins** because it has the highest precedence.
2. If no command-line value was given, Terraform would use `instance_type = "t2.nano"` from `02-production.auto.tfvars`.
3. If `.auto.tfvars` files were missing, it would use `t2.small` from `terraform.tfvars.json`.
4. If `.tfvars.json` was missing, it would use `t2.medium` from `terraform.tfvars`.
5. If no `.tfvars` file existed, it would use the environment variable (`t2.large`).

---

## **Key Takeaways**
- **Later sources in the list override earlier ones.**
- **Command-line values (`-var`) have the highest precedence.**
- **Use `.auto.tfvars` for automatic loading, processed in lexical order.**
- **Use environment variables (`TF_VAR_`) for automation.**
- **Default `terraform.tfvars` and `.tfvars.json` are loaded automatically.**


