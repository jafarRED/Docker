# Terraform Data Types

Terraform data types are essential for defining and structuring the configuration to manage infrastructure. Understanding the data types in Terraform helps in managing variables, outputs, and resources more effectively.

## 1. Basic Data Types

### **String**
**Description:** A string represents a sequence of characters.

**Example:**
```hcl
variable "example_string" {
  type    = string
  default = "Hello, Terraform!"
}
```

### **Number**
**Description:** A number represents an integer or floating-point number.

**Example:**
```hcl
variable "example_number" {
  type    = number
  default = 42
}
```

### **Boolean**
**Description:** A boolean represents a true/false value.

**Example:**
```hcl
variable "example_boolean" {
  type    = bool
  default = true
}
```

## 2. Complex Data Types

### **List**
**Description:** A list is an ordered collection of values. All elements in a list must be of the same type.

**Example:**
```hcl
variable "example_list" {
  type    = list(string)
  default = ["apple", "banana", "cherry"]
}
```

**Operations on Lists:**
- Access elements using an index (e.g., `var.example_list[0]`).
- Supports functions like `length()`, `join()`, and `distinct()`.

### **Set**
**Description:** A set is an unordered collection of unique values. Unlike lists, sets do not allow duplicates.

**Example:**
```hcl
variable "example_set" {
  type    = set(string)
  default = ["apple", "banana", "apple"]  # "apple" appears only once
}
```

**Operations on Sets:**
- Supports functions like `length()`, `union()`, `intersection()`, and `difference()`.

### **Map**
**Description:** A map is a collection of key-value pairs. Keys must be unique, and each key is associated with a value of a specified type.

**Example:**
```hcl
variable "example_map" {
  type    = map(string)
  default = {
    "name" = "John"
    "age"  = "30"
  }
}
```

**Operations on Maps:**
- Access values using keys (e.g., `var.example_map["name"]`).
- Supports `length()`, `keys()`, and `values()` functions.

## 3. Object

**Description:** An object is an unordered collection of named attributes with specific types.

**Example:**
```hcl
variable "example_object" {
  type = object({
    name   = string
    age    = number
    active = bool
  })
  default = {
    name   = "John"
    age    = 30
    active = true
  }
}
```

**Operations on Objects:**
- Access individual attributes (e.g., `var.example_object.name`).
- Supports `length()`, `keys()`, and `values()`.

## 4. Tuple

**Description:** A tuple is an ordered collection of elements of different types.

**Example:**
```hcl
variable "example_tuple" {
  type    = tuple([string, number, bool])
  default = ["John", 30, true]
}
```

**Operations on Tuples:**
- Access elements using an index (e.g., `var.example_tuple[0]`).
- Supports `length()` function.

## 5. Special Types

### **Any**
**Description:** The `any` type allows for a value of any type (string, number, list, map, etc.).

**Example:**
```hcl
variable "example_any" {
  type    = any
  default = "Hello"
}
```

**Use Case:** Useful for flexible variables but should be used cautiously.

### **Null**
**Description:** Represents the absence of a value.

**Example:**
```hcl
variable "example_null" {
  type    = string
  default = null
}
```

**Use Case:** Helps in defining optional variables.

## 6. Dynamic Blocks
Terraform allows dynamically creating blocks like resources using `for_each` or `count`.

**Example:**
```hcl
variable "services" {
  type = list(object({
    name     = string
    instance = string
  }))
}

resource "aws_instance" "services" {
  for_each = { for service in var.services : service.name => service }

  instance_type = each.value.instance
  ami           = "ami-123456"
  tags = {
    Name = each.value.name
  }
}
```

## **Summary of Common Terraform Data Types**

| Data Type | Description | Example |
|-----------|-------------|---------|
| **String** | A sequence of characters. | `"Hello, Terraform!"` |
| **Number** | An integer or floating-point number. | `42` or `3.14` |
| **Boolean** | A true/false value. | `true` or `false` |
| **List** | An ordered collection of values of the same type. | `["apple", "banana", "cherry"]` |
| **Set** | An unordered collection of unique values. | `set(["apple", "banana"])` |
| **Map** | A collection of key-value pairs with unique keys. | `{ "name" = "John", "age" = 30 }` |
| **Object** | A collection of named attributes with specified types. | `{ "name" = "John", "age" = 30 }` |
| **Tuple** | An ordered collection of elements with different types. | `tuple(["John", 30, true])` |
| **Any** | A flexible value of any type. | `"Hello"`, `42`, `true` |
| **Null** | Represents the absence of a value. | `null` |



