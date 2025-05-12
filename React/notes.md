# Props drilling

Passing data from parent to child then child 1 to child 2 and so on....

```
# Controlled and Uncontrolled components 

There is not an exactly definition for this but if you are controlling a child component using parent component then parent component is known as a controlled component.

# Lifting the state up
For eg accordion if there are 4 accordion and you want when you try to expand anyone then other one which is already expanded should be close and the new one will only expand. For that we can use useState and pass the set function by parent component to the child component and whenever it will called by the index that only will be expand. (for more detailed video checkout the episode 11 data is the new oil)
