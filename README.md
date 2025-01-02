# Terraform_notes
This is my own prepared notes on Terraform


#learning HCL

/*- this will make multiple lines as COMMENT
this is 
a multiline
comment */

#Block
/*Block is a container for other content. 
Blocks are defined by their type and enclosed in curly braces {}

there are various types of blocks, Provider block, Data Block, resource block, variable block */

block_type {
  attribute 1 = value1
  attribute 2 = value 2

}

resource "aws_instance" "Demo" {
    ami = "ami-0a91cd140a1fc148a"
    instance_type = "t2.micro"
    count = 3
    enabled = true
  
}

#Attributes

key = value 
#so in above example, resouce block we wrote, ami,instance, count and enabled are the Attributes.


#Datatypes
# different data types in HCL, so 
"string" which is in doble quotes
number 
boolean true false


List
/* list can be of security group, subnet, servers, databases and so much more
List is always defined in [] square brackets */

List = ["item1", "item2", "item3"]

security_groups = ["sg-1234", "sg-2345", "sg-3456"]

#the above was the example of a List of security groups.


Maps
#in HCL Maps are defined using Curly brackets and they follwo the key value syntex similar to dictionaries in Python and other programming language
 variable "example_map" {
    type = Map
    default = {key1 = "value1", key2 = "value2", key3 = "value3"}
 }
 #so in above example, we have Variable block, defined as Data Type Map and last line is the Key value pair.
 #this key value pair can have different data types, strings, boolean types in it.

 locals {
    my_map = {name = "Demi S", age = 35, admin = true}

 }

 #so from above example, if we want to get value to age, then the command to get this is as below 
 locals.my_map["age"]


#condition
/*Conditions are very important in HCL to make decisions or to execute  a certain block of code and there can be various scenario
you might be using conditions, */

#so if you want to give a condition like, if the environment is devlopment, then launch t2.micro instance, or else t2.small

resource "aws_instance" "server" {
    instance_type = var.environment == "development" ? "t2.micro" : "t2.small"

}

#functions
#functions help you to perform operations calculations and transformations within your code
#and HCL provides you with so many different fucntions that you can use to maniulate data and validate inputs and many more

#Recoursedependency
/* it's used to create relationship between two resources,
and also to define their order and how it should be created

Let's take an example, you have an instance and a security group created separately. But you want to use that SG with this Instance
Example to d that is as below - */

resource aws_instance "name" {
ami = mmmmmmm
instance_type = t2.micro
vpc_security_group_id = aws_security_group.mysg.id

}

resource aws_security_group "mysg" {

}
