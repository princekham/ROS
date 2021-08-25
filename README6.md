<H4>36. Write a Python Publisher</H4>

- Go to your package directory -> create a file named "robot_news_station.py"
- And make it executable (to use with similink)

```
cd ros2_ws/src/my_py_pkg/my_py_pkg
touch robot_news_station.py
chmod +x robot_news_station.py
 ```
- copy from python template file and modify it as follow

```
```
- Node name and the file name can be identical or different
- And add a new line in the setup.py
- "robot_news_station=my_py_pkg.robot_news_station"
- where the first robot_news_station is the name of the executable
- And the later is the name of the file followed by where to start : main
- 
- don't forget to put   <depend>example_interfaces</depend> in the package.xml
- 



