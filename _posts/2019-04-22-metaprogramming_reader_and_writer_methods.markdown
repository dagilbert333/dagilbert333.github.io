---
layout: post
title:      "Metaprogramming Reader and Writer Methods"
date:       2019-04-22 01:06:58 -0400
permalink:  metaprogramming_reader_and_writer_methods
---


**Using Macros:**

```
class Dog
  attr_accessor :name, :breed, :owner

  def twinsies?
    true if self.owner.name == self.name
  end
	
end
```

**Build out our own reader and writer methods with metaprogramming.**

```
class Dog

#longhand building set and get methods with metaprogramming
 
 def self.define_properties(props)
   props.each do |prop|
	 
     # Defining the reader
    
		define_method(prop) do
       
			 # What does this reader need to do?
       # It needs to expose the instance variable
       
			 instance_variable_get(:"@#{prop}")
     end
		 
     # Defining the writer
    
		define_method("#{prop}=") do |arg|
     
		 # What does this reader need to do?
     # It needs to expose the instance variable
     
		 instance_variable_set(:"@#{prop}", arg)
     end
   end
	 
	  self.define_properties([:name, :breed])
 end
 

class Owner
  attr_accessor :name
end

fido = Dog.new
fido.name = "FIDO"
david = Owner.new
david.name = "DAVID"
fido.owner = david
```

To Be Continued...

