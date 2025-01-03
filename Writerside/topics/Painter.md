# Painter

## 默认绘图风格类（DefaultPainter）

`Models_in_one.utilis.painter`模块提供类`DefaultPainter`，用于将绘图风格转化为默认的绘图风格。

**导入方法：**
```python 
from Models_in_one.utilis.painter import DefaultPainter
```

在使用时，请使用Python提供的上下文管理器, `with `语句块中的绘图内容将会被设置为默认的绘图风格：
```Python
from matplotlib import pyplot as plt
from Models_in_one.utilis.painter import DefaultPainter


with DefaultPainter(plt, fig_size=(7, 7)) as default_painter:
    ...  # Draw here, use default_painter instead of plt.figure
    
    default_painter.show()
    
plt.show()  # it's ok
```
当在语句块外部开始绘图时，请显式提供如下代码：
```Python
plt.figure(...)
```

## 颜色设置

<deflist collapsible="true">
    <def title="color_int(index)">
    按序号返回给定颜色RBG（0-255）
    </def>
    <def title="color_float(index)">
    按序号返回给定颜色RBG（0.0-1.0）
    </def>
    <def title="int_to_hex(color)">
    将（0-255）的RGB颜色转化为HEX颜色
    </def>
    <def title="float_to_hex(color)">
    将（0.0-1.0）的RGB颜色转化为HEX颜色
    </def>
    <def title="hex_to_int(hex_color)">
    将HEX颜色转化为（0-255）的RGB颜色
    </def>
    <def title="hex_to_float(hex_color)">
    将HEX颜色转化为（0.0-1.0）的RGB颜色
    </def>
    <def title="gradient_color_generator(color_1, color_2, total_num, need_float=True)">
    返回两种颜色之间的渐变色的生成器
    </def>
</deflist>

`Models_in_one.utilis.painter`中索引与颜色对应如下表：

<table>
<tr><td>序号</td><td>颜色</td><td>HEX</td><td>RGB</td></tr>
<tr><td>1</td><td><img src="https://placehold.co/15x15/000000/000000.png" alt="s"/></td><td>#000000</td><td>(0, 0, 0)</td></tr>
<tr><td>2</td><td><img src="https://placehold.co/15x15/8b8b8b/8b8b8b.png" alt="s"/></td><td>#8b8b8b</td><td>(139, 139, 139)</td></tr>
<tr><td>3</td><td><img src="https://placehold.co/15x15/a0a0a0/a0a0a0.png" alt="s"/></td><td>#a0a0a0</td><td>(160, 160, 160)</td></tr>
<tr><td>4</td><td><img src="https://placehold.co/15x15/c0c0c0/c0c0c0.png" alt="s"/></td><td>#c0c0c0</td><td>(192, 192, 192)</td></tr>
<tr><td>5</td><td><img src="https://placehold.co/15x15/d3d3d3/d3d3d3.png" alt="s"/></td><td>#d3d3d3</td><td>(211, 211, 211)</td></tr>
<tr><td>6</td><td><img src="https://placehold.co/15x15/e1e1e1/e1e1e1.png" alt="s"/></td><td>#e1e1e1</td><td>(225, 225, 225)</td></tr>
<tr><td>7</td><td><img src="https://placehold.co/15x15/e7e7e7/e7e7e7.png" alt="s"/></td><td>#e7e7e7</td><td>(231, 231, 231)</td></tr>
<tr><td>8</td><td><img src="https://placehold.co/15x15/f7f7f7/f7f7f7.png" alt="s"/></td><td>#f7f7f7</td><td>(247, 247, 247)</td></tr>
<tr><td>9</td><td><img src="https://placehold.co/15x15/fff9f9/fff9f9.png" alt="s"/></td><td>#fff9f9</td><td>(255, 249, 249)</td></tr>
<tr><td>10</td><td><img src="https://placehold.co/15x15/bb8e8e/bb8e8e.png" alt="s"/></td><td>#bb8e8e</td><td>(187, 142, 142)</td></tr>
<tr><td>11</td><td><img src="https://placehold.co/15x15/ef8080/ef8080.png" alt="s"/></td><td>#ef8080</td><td>(239, 128, 128)</td></tr>
<tr><td>12</td><td><img src="https://placehold.co/15x15/cd5b5b/cd5b5b.png" alt="s"/></td><td>#cd5b5b</td><td>(205, 91, 91)</td></tr>
<tr><td>13</td><td><img src="https://placehold.co/15x15/a52929/a52929.png" alt="s"/></td><td>#a52929</td><td>(165, 41, 41)</td></tr>
<tr><td>14</td><td><img src="https://placehold.co/15x15/b22121/b22121.png" alt="s"/></td><td>#b22121</td><td>(178, 33, 33)</td></tr>
<tr><td>15</td><td><img src="https://placehold.co/15x15/800000/800000.png" alt="s"/></td><td>#800000</td><td>(128, 0, 0)</td></tr>
<tr><td>16</td><td><img src="https://placehold.co/15x15/8a0000/8a0000.png" alt="s"/></td><td>#8a0000</td><td>(138, 0, 0)</td></tr>
<tr><td>17</td><td><img src="https://placehold.co/15x15/ff0000/ff0000.png" alt="s"/></td><td>#ff0000</td><td>(255, 0, 0)</td></tr>
<tr><td>18</td><td><img src="https://placehold.co/15x15/ffe4e1/ffe4e1.png" alt="s"/></td><td>#ffe4e1</td><td>(255, 228, 225)</td></tr>
<tr><td>19</td><td><img src="https://placehold.co/15x15/f98072/f98072.png" alt="s"/></td><td>#f98072</td><td>(249, 128, 114)</td></tr>
<tr><td>20</td><td><img src="https://placehold.co/15x15/ff6247/ff6247.png" alt="s"/></td><td>#ff6247</td><td>(255, 98, 71)</td></tr>
<tr><td>21</td><td><img src="https://placehold.co/15x15/e8957a/e8957a.png" alt="s"/></td><td>#e8957a</td><td>(232, 149, 122)</td></tr>
<tr><td>22</td><td><img src="https://placehold.co/15x15/ff7f4f/ff7f4f.png" alt="s"/></td><td>#ff7f4f</td><td>(255, 127, 79)</td></tr>
<tr><td>23</td><td><img src="https://placehold.co/15x15/ff4500/ff4500.png" alt="s"/></td><td>#ff4500</td><td>(255, 69, 0)</td></tr>
<tr><td>24</td><td><img src="https://placehold.co/15x15/ffa07a/ffa07a.png" alt="s"/></td><td>#ffa07a</td><td>(255, 160, 122)</td></tr>
<tr><td>25</td><td><img src="https://placehold.co/15x15/a0512c/a0512c.png" alt="s"/></td><td>#a0512c</td><td>(160, 81, 44)</td></tr>
<tr><td>26</td><td><img src="https://placehold.co/15x15/fff4ed/fff4ed.png" alt="s"/></td><td>#fff4ed</td><td>(255, 244, 237)</td></tr>
<tr><td>27</td><td><img src="https://placehold.co/15x15/d2691d/d2691d.png" alt="s"/></td><td>#d2691d</td><td>(210, 105, 29)</td></tr>
<tr><td>28</td><td><img src="https://placehold.co/15x15/8a4512/8a4512.png" alt="s"/></td><td>#8a4512</td><td>(138, 69, 18)</td></tr>
<tr><td>29</td><td><img src="https://placehold.co/15x15/f3a45f/f3a45f.png" alt="s"/></td><td>#f3a45f</td><td>(243, 164, 95)</td></tr>
<tr><td>30</td><td><img src="https://placehold.co/15x15/ffdab8/ffdab8.png" alt="s"/></td><td>#ffdab8</td><td>(255, 218, 184)</td></tr>
<tr><td>31</td><td><img src="https://placehold.co/15x15/cd843f/cd843f.png" alt="s"/></td><td>#cd843f</td><td>(205, 132, 63)</td></tr>
<tr><td>32</td><td><img src="https://placehold.co/15x15/f9efe6/f9efe6.png" alt="s"/></td><td>#f9efe6</td><td>(249, 239, 230)</td></tr>
<tr><td>33</td><td><img src="https://placehold.co/15x15/ffe4c3/ffe4c3.png" alt="s"/></td><td>#ffe4c3</td><td>(255, 228, 195)</td></tr>
<tr><td>34</td><td><img src="https://placehold.co/15x15/ff8b00/ff8b00.png" alt="s"/></td><td>#ff8b00</td><td>(255, 139, 0)</td></tr>
<tr><td>35</td><td><img src="https://placehold.co/15x15/deb786/deb786.png" alt="s"/></td><td>#deb786</td><td>(222, 183, 134)</td></tr>
<tr><td>36</td><td><img src="https://placehold.co/15x15/f9ead7/f9ead7.png" alt="s"/></td><td>#f9ead7</td><td>(249, 234, 215)</td></tr>
<tr><td>37</td><td><img src="https://placehold.co/15x15/d2b48b/d2b48b.png" alt="s"/></td><td>#d2b48b</td><td>(210, 180, 139)</td></tr>
<tr><td>38</td><td><img src="https://placehold.co/15x15/ffdead/ffdead.png" alt="s"/></td><td>#ffdead</td><td>(255, 222, 173)</td></tr>
<tr><td>39</td><td><img src="https://placehold.co/15x15/ffeacd/ffeacd.png" alt="s"/></td><td>#ffeacd</td><td>(255, 234, 205)</td></tr>
<tr><td>40</td><td><img src="https://placehold.co/15x15/ffeed5/ffeed5.png" alt="s"/></td><td>#ffeed5</td><td>(255, 238, 213)</td></tr>
<tr><td>41</td><td><img src="https://placehold.co/15x15/ffe4b5/ffe4b5.png" alt="s"/></td><td>#ffe4b5</td><td>(255, 228, 181)</td></tr>
<tr><td>42</td><td><img src="https://placehold.co/15x15/ffa500/ffa500.png" alt="s"/></td><td>#ffa500</td><td>(255, 165, 0)</td></tr>
<tr><td>43</td><td><img src="https://placehold.co/15x15/f4deb2/f4deb2.png" alt="s"/></td><td>#f4deb2</td><td>(244, 222, 178)</td></tr>
<tr><td>44</td><td><img src="https://placehold.co/15x15/fcf4e6/fcf4e6.png" alt="s"/></td><td>#fcf4e6</td><td>(252, 244, 230)</td></tr>
<tr><td>45</td><td><img src="https://placehold.co/15x15/fff9ef/fff9ef.png" alt="s"/></td><td>#fff9ef</td><td>(255, 249, 239)</td></tr>
<tr><td>46</td><td><img src="https://placehold.co/15x15/b7850b/b7850b.png" alt="s"/></td><td>#b7850b</td><td>(183, 133, 11)</td></tr>
<tr><td>47</td><td><img src="https://placehold.co/15x15/daa51f/daa51f.png" alt="s"/></td><td>#daa51f</td><td>(218, 165, 31)</td></tr>
<tr><td>48</td><td><img src="https://placehold.co/15x15/fff7dc/fff7dc.png" alt="s"/></td><td>#fff7dc</td><td>(255, 247, 220)</td></tr>
<tr><td>49</td><td><img src="https://placehold.co/15x15/ffd700/ffd700.png" alt="s"/></td><td>#ffd700</td><td>(255, 215, 0)</td></tr>
<tr><td>50</td><td><img src="https://placehold.co/15x15/fff9cd/fff9cd.png" alt="s"/></td><td>#fff9cd</td><td>(255, 249, 205)</td></tr>
<tr><td>51</td><td><img src="https://placehold.co/15x15/efe68b/efe68b.png" alt="s"/></td><td>#efe68b</td><td>(239, 230, 139)</td></tr>
<tr><td>52</td><td><img src="https://placehold.co/15x15/ede7aa/ede7aa.png" alt="s"/></td><td>#ede7aa</td><td>(237, 231, 170)</td></tr>
<tr><td>53</td><td><img src="https://placehold.co/15x15/bcb66b/bcb66b.png" alt="s"/></td><td>#bcb66b</td><td>(188, 182, 107)</td></tr>
<tr><td>54</td><td><img src="https://placehold.co/15x15/ffffef/ffffef.png" alt="s"/></td><td>#ffffef</td><td>(255, 255, 239)</td></tr>
<tr><td>55</td><td><img src="https://placehold.co/15x15/f4f4dc/f4f4dc.png" alt="s"/></td><td>#f4f4dc</td><td>(244, 244, 220)</td></tr>
<tr><td>56</td><td><img src="https://placehold.co/15x15/ffffe0/ffffe0.png" alt="s"/></td><td>#ffffe0</td><td>(255, 255, 224)</td></tr>
<tr><td>57</td><td><img src="https://placehold.co/15x15/f9f9d2/f9f9d2.png" alt="s"/></td><td>#f9f9d2</td><td>(249, 249, 210)</td></tr>
<tr><td>58</td><td><img src="https://placehold.co/15x15/808000/808000.png" alt="s"/></td><td>#808000</td><td>(128, 128, 0)</td></tr>
<tr><td>59</td><td><img src="https://placehold.co/15x15/bebe00/bebe00.png" alt="s"/></td><td>#bebe00</td><td>(190, 190, 0)</td></tr>
<tr><td>60</td><td><img src="https://placehold.co/15x15/ffff00/ffff00.png" alt="s"/></td><td>#ffff00</td><td>(255, 255, 0)</td></tr>
<tr><td>61</td><td><img src="https://placehold.co/15x15/6b8d22/6b8d22.png" alt="s"/></td><td>#6b8d22</td><td>(107, 141, 34)</td></tr>
<tr><td>62</td><td><img src="https://placehold.co/15x15/9acd31/9acd31.png" alt="s"/></td><td>#9acd31</td><td>(154, 205, 49)</td></tr>
<tr><td>63</td><td><img src="https://placehold.co/15x15/546b2e/546b2e.png" alt="s"/></td><td>#546b2e</td><td>(84, 107, 46)</td></tr>
<tr><td>64</td><td><img src="https://placehold.co/15x15/adff2e/adff2e.png" alt="s"/></td><td>#adff2e</td><td>(173, 255, 46)</td></tr>
<tr><td>65</td><td><img src="https://placehold.co/15x15/7fff00/7fff00.png" alt="s"/></td><td>#7fff00</td><td>(127, 255, 0)</td></tr>
<tr><td>66</td><td><img src="https://placehold.co/15x15/7cfb00/7cfb00.png" alt="s"/></td><td>#7cfb00</td><td>(124, 251, 0)</td></tr>
<tr><td>67</td><td><img src="https://placehold.co/15x15/efffef/efffef.png" alt="s"/></td><td>#efffef</td><td>(239, 255, 239)</td></tr>
<tr><td>68</td><td><img src="https://placehold.co/15x15/8ebb8e/8ebb8e.png" alt="s"/></td><td>#8ebb8e</td><td>(142, 187, 142)</td></tr>
<tr><td>69</td><td><img src="https://placehold.co/15x15/98fb98/98fb98.png" alt="s"/></td><td>#98fb98</td><td>(152, 251, 152)</td></tr>
<tr><td>70</td><td><img src="https://placehold.co/15x15/8fed8f/8fed8f.png" alt="s"/></td><td>#8fed8f</td><td>(143, 237, 143)</td></tr>
<tr><td>71</td><td><img src="https://placehold.co/15x15/218a21/218a21.png" alt="s"/></td><td>#218a21</td><td>(33, 138, 33)</td></tr>
<tr><td>72</td><td><img src="https://placehold.co/15x15/31cd31/31cd31.png" alt="s"/></td><td>#31cd31</td><td>(49, 205, 49)</td></tr>
<tr><td>73</td><td><img src="https://placehold.co/15x15/006300/006300.png" alt="s"/></td><td>#006300</td><td>(0, 99, 0)</td></tr>
<tr><td>74</td><td><img src="https://placehold.co/15x15/008000/008000.png" alt="s"/></td><td>#008000</td><td>(0, 128, 0)</td></tr>
<tr><td>75</td><td><img src="https://placehold.co/15x15/00ff00/00ff00.png" alt="s"/></td><td>#00ff00</td><td>(0, 255, 0)</td></tr>
<tr><td>76</td><td><img src="https://placehold.co/15x15/2d8a56/2d8a56.png" alt="s"/></td><td>#2d8a56</td><td>(45, 138, 86)</td></tr>
<tr><td>77</td><td><img src="https://placehold.co/15x15/3cb271/3cb271.png" alt="s"/></td><td>#3cb271</td><td>(60, 178, 113)</td></tr>
<tr><td>78</td><td><img src="https://placehold.co/15x15/00ff7f/00ff7f.png" alt="s"/></td><td>#00ff7f</td><td>(0, 255, 127)</td></tr>
<tr><td>79</td><td><img src="https://placehold.co/15x15/f4fff9/f4fff9.png" alt="s"/></td><td>#f4fff9</td><td>(244, 255, 249)</td></tr>
<tr><td>80</td><td><img src="https://placehold.co/15x15/00f99a/00f99a.png" alt="s"/></td><td>#00f99a</td><td>(0, 249, 154)</td></tr>
<tr><td>81</td><td><img src="https://placehold.co/15x15/66cdaa/66cdaa.png" alt="s"/></td><td>#66cdaa</td><td>(102, 205, 170)</td></tr>
<tr><td>82</td><td><img src="https://placehold.co/15x15/7fffd4/7fffd4.png" alt="s"/></td><td>#7fffd4</td><td>(127, 255, 212)</td></tr>
<tr><td>83</td><td><img src="https://placehold.co/15x15/40e0d0/40e0d0.png" alt="s"/></td><td>#40e0d0</td><td>(64, 224, 208)</td></tr>
<tr><td>84</td><td><img src="https://placehold.co/15x15/1fb2aa/1fb2aa.png" alt="s"/></td><td>#1fb2aa</td><td>(31, 178, 170)</td></tr>
<tr><td>85</td><td><img src="https://placehold.co/15x15/48d1cc/48d1cc.png" alt="s"/></td><td>#48d1cc</td><td>(72, 209, 204)</td></tr>
<tr><td>86</td><td><img src="https://placehold.co/15x15/efffff/efffff.png" alt="s"/></td><td>#efffff</td><td>(239, 255, 255)</td></tr>
<tr><td>87</td><td><img src="https://placehold.co/15x15/e0ffff/e0ffff.png" alt="s"/></td><td>#e0ffff</td><td>(224, 255, 255)</td></tr>
<tr><td>88</td><td><img src="https://placehold.co/15x15/afeded/afeded.png" alt="s"/></td><td>#afeded</td><td>(175, 237, 237)</td></tr>
<tr><td>89</td><td><img src="https://placehold.co/15x15/2e4e4e/2e4e4e.png" alt="s"/></td><td>#2e4e4e</td><td>(46, 78, 78)</td></tr>
<tr><td>90</td><td><img src="https://placehold.co/15x15/008080/008080.png" alt="s"/></td><td>#008080</td><td>(0, 128, 128)</td></tr>
<tr><td>91</td><td><img src="https://placehold.co/15x15/008a8a/008a8a.png" alt="s"/></td><td>#008a8a</td><td>(0, 138, 138)</td></tr>
<tr><td>92</td><td><img src="https://placehold.co/15x15/00bebe/00bebe.png" alt="s"/></td><td>#00bebe</td><td>(0, 190, 190)</td></tr>
<tr><td>93</td><td><img src="https://placehold.co/15x15/00ffff/00ffff.png" alt="s"/></td><td>#00ffff</td><td>(0, 255, 255)</td></tr>
<tr><td>94</td><td><img src="https://placehold.co/15x15/00ced1/00ced1.png" alt="s"/></td><td>#00ced1</td><td>(0, 206, 209)</td></tr>
<tr><td>95</td><td><img src="https://placehold.co/15x15/5e9ea0/5e9ea0.png" alt="s"/></td><td>#5e9ea0</td><td>(94, 158, 160)</td></tr>
<tr><td>96</td><td><img src="https://placehold.co/15x15/b0e0e6/b0e0e6.png" alt="s"/></td><td>#b0e0e6</td><td>(176, 224, 230)</td></tr>
<tr><td>97</td><td><img src="https://placehold.co/15x15/add8e6/add8e6.png" alt="s"/></td><td>#add8e6</td><td>(173, 216, 230)</td></tr>
<tr><td>98</td><td><img src="https://placehold.co/15x15/00beff/00beff.png" alt="s"/></td><td>#00beff</td><td>(0, 190, 255)</td></tr>
<tr><td>99</td><td><img src="https://placehold.co/15x15/86ceea/86ceea.png" alt="s"/></td><td>#86ceea</td><td>(134, 206, 234)</td></tr>
<tr><td>100</td><td><img src="https://placehold.co/15x15/86cef9/86cef9.png" alt="s"/></td><td>#86cef9</td><td>(134, 206, 249)</td></tr>
<tr><td>101</td><td><img src="https://placehold.co/15x15/4681b4/4681b4.png" alt="s"/></td><td>#4681b4</td><td>(70, 129, 180)</td></tr>
<tr><td>102</td><td><img src="https://placehold.co/15x15/eff7ff/eff7ff.png" alt="s"/></td><td>#eff7ff</td><td>(239, 247, 255)</td></tr>
<tr><td>103</td><td><img src="https://placehold.co/15x15/1d8fff/1d8fff.png" alt="s"/></td><td>#1d8fff</td><td>(29, 143, 255)</td></tr>
<tr><td>104</td><td><img src="https://placehold.co/15x15/778799/778799.png" alt="s"/></td><td>#778799</td><td>(119, 135, 153)</td></tr>
<tr><td>105</td><td><img src="https://placehold.co/15x15/70808f/70808f.png" alt="s"/></td><td>#70808f</td><td>(112, 128, 143)</td></tr>
<tr><td>106</td><td><img src="https://placehold.co/15x15/b0c3de/b0c3de.png" alt="s"/></td><td>#b0c3de</td><td>(176, 195, 222)</td></tr>
<tr><td>107</td><td><img src="https://placehold.co/15x15/6394ec/6394ec.png" alt="s"/></td><td>#6394ec</td><td>(99, 148, 236)</td></tr>
<tr><td>108</td><td><img src="https://placehold.co/15x15/4169e1/4169e1.png" alt="s"/></td><td>#4169e1</td><td>(65, 105, 225)</td></tr>
<tr><td>109</td><td><img src="https://placehold.co/15x15/f7f7ff/f7f7ff.png" alt="s"/></td><td>#f7f7ff</td><td>(247, 247, 255)</td></tr>
<tr><td>110</td><td><img src="https://placehold.co/15x15/e6e6f9/e6e6f9.png" alt="s"/></td><td>#e6e6f9</td><td>(230, 230, 249)</td></tr>
<tr><td>111</td><td><img src="https://placehold.co/15x15/181870/181870.png" alt="s"/></td><td>#181870</td><td>(24, 24, 112)</td></tr>
<tr><td>112</td><td><img src="https://placehold.co/15x15/000080/000080.png" alt="s"/></td><td>#000080</td><td>(0, 0, 128)</td></tr>
<tr><td>113</td><td><img src="https://placehold.co/15x15/00008a/00008a.png" alt="s"/></td><td>#00008a</td><td>(0, 0, 138)</td></tr>
<tr><td>114</td><td><img src="https://placehold.co/15x15/0000cd/0000cd.png" alt="s"/></td><td>#0000cd</td><td>(0, 0, 205)</td></tr>
<tr><td>115</td><td><img src="https://placehold.co/15x15/0000ff/0000ff.png" alt="s"/></td><td>#0000ff</td><td>(0, 0, 255)</td></tr>
<tr><td>116</td><td><img src="https://placehold.co/15x15/6a59cd/6a59cd.png" alt="s"/></td><td>#6a59cd</td><td>(106, 89, 205)</td></tr>
<tr><td>117</td><td><img src="https://placehold.co/15x15/483d8a/483d8a.png" alt="s"/></td><td>#483d8a</td><td>(72, 61, 138)</td></tr>
<tr><td>118</td><td><img src="https://placehold.co/15x15/7b68ed/7b68ed.png" alt="s"/></td><td>#7b68ed</td><td>(123, 104, 237)</td></tr>
<tr><td>119</td><td><img src="https://placehold.co/15x15/9270db/9270db.png" alt="s"/></td><td>#9270db</td><td>(146, 112, 219)</td></tr>
<tr><td>120</td><td><img src="https://placehold.co/15x15/663399/663399.png" alt="s"/></td><td>#663399</td><td>(102, 51, 153)</td></tr>
<tr><td>121</td><td><img src="https://placehold.co/15x15/892ae2/892ae2.png" alt="s"/></td><td>#892ae2</td><td>(137, 42, 226)</td></tr>
<tr><td>122</td><td><img src="https://placehold.co/15x15/4b0081/4b0081.png" alt="s"/></td><td>#4b0081</td><td>(75, 0, 129)</td></tr>
<tr><td>123</td><td><img src="https://placehold.co/15x15/9931cc/9931cc.png" alt="s"/></td><td>#9931cc</td><td>(153, 49, 204)</td></tr>
<tr><td>124</td><td><img src="https://placehold.co/15x15/9300d3/9300d3.png" alt="s"/></td><td>#9300d3</td><td>(147, 0, 211)</td></tr>
<tr><td>125</td><td><img src="https://placehold.co/15x15/b954d3/b954d3.png" alt="s"/></td><td>#b954d3</td><td>(185, 84, 211)</td></tr>
<tr><td>126</td><td><img src="https://placehold.co/15x15/d8bed8/d8bed8.png" alt="s"/></td><td>#d8bed8</td><td>(216, 190, 216)</td></tr>
<tr><td>127</td><td><img src="https://placehold.co/15x15/dda0dd/dda0dd.png" alt="s"/></td><td>#dda0dd</td><td>(221, 160, 221)</td></tr>
<tr><td>128</td><td><img src="https://placehold.co/15x15/ed81ed/ed81ed.png" alt="s"/></td><td>#ed81ed</td><td>(237, 129, 237)</td></tr>
<tr><td>129</td><td><img src="https://placehold.co/15x15/800080/800080.png" alt="s"/></td><td>#800080</td><td>(128, 0, 128)</td></tr>
<tr><td>130</td><td><img src="https://placehold.co/15x15/8a008a/8a008a.png" alt="s"/></td><td>#8a008a</td><td>(138, 0, 138)</td></tr>
<tr><td>131</td><td><img src="https://placehold.co/15x15/be00be/be00be.png" alt="s"/></td><td>#be00be</td><td>(190, 0, 190)</td></tr>
<tr><td>132</td><td><img src="https://placehold.co/15x15/ff00ff/ff00ff.png" alt="s"/></td><td>#ff00ff</td><td>(255, 0, 255)</td></tr>
<tr><td>133</td><td><img src="https://placehold.co/15x15/da70d6/da70d6.png" alt="s"/></td><td>#da70d6</td><td>(218, 112, 214)</td></tr>
<tr><td>134</td><td><img src="https://placehold.co/15x15/c61584/c61584.png" alt="s"/></td><td>#c61584</td><td>(198, 21, 132)</td></tr>
<tr><td>135</td><td><img src="https://placehold.co/15x15/ff1492/ff1492.png" alt="s"/></td><td>#ff1492</td><td>(255, 20, 146)</td></tr>
<tr><td>136</td><td><img src="https://placehold.co/15x15/ff69b4/ff69b4.png" alt="s"/></td><td>#ff69b4</td><td>(255, 105, 180)</td></tr>
<tr><td>137</td><td><img src="https://placehold.co/15x15/ffeff4/ffeff4.png" alt="s"/></td><td>#ffeff4</td><td>(255, 239, 244)</td></tr>
<tr><td>138</td><td><img src="https://placehold.co/15x15/db7092/db7092.png" alt="s"/></td><td>#db7092</td><td>(219, 112, 146)</td></tr>
<tr><td>139</td><td><img src="https://placehold.co/15x15/dc143c/dc143c.png" alt="s"/></td><td>#dc143c</td><td>(220, 20, 60)</td></tr>
<tr><td>140</td><td><img src="https://placehold.co/15x15/ffbfcb/ffbfcb.png" alt="s"/></td><td>#ffbfcb</td><td>(255, 191, 203)</td></tr>
<tr><td>141</td><td><img src="https://placehold.co/15x15/ffb5c0/ffb5c0.png" alt="s"/></td><td>#ffb5c0</td><td>(255, 181, 192)</td></tr>
<tr><td>142</td><td><img src="https://placehold.co/15x15/fbb4ae/fbb4ae.png" alt="s"/></td><td>#fbb4ae</td><td>(251, 180, 174)</td></tr>
<tr><td>143</td><td><img src="https://placehold.co/15x15/b2cde3/b2cde3.png" alt="s"/></td><td>#b2cde3</td><td>(178, 205, 227)</td></tr>
<tr><td>144</td><td><img src="https://placehold.co/15x15/cceac4/cceac4.png" alt="s"/></td><td>#cceac4</td><td>(204, 234, 196)</td></tr>
<tr><td>145</td><td><img src="https://placehold.co/15x15/decbe4/decbe4.png" alt="s"/></td><td>#decbe4</td><td>(222, 203, 228)</td></tr>
<tr><td>146</td><td><img src="https://placehold.co/15x15/fed9a6/fed9a6.png" alt="s"/></td><td>#fed9a6</td><td>(254, 217, 166)</td></tr>
<tr><td>147</td><td><img src="https://placehold.co/15x15/ffffcc/ffffcc.png" alt="s"/></td><td>#ffffcc</td><td>(255, 255, 204)</td></tr>
<tr><td>148</td><td><img src="https://placehold.co/15x15/e5d8bc/e5d8bc.png" alt="s"/></td><td>#e5d8bc</td><td>(229, 216, 188)</td></tr>
<tr><td>149</td><td><img src="https://placehold.co/15x15/fcdaeb/fcdaeb.png" alt="s"/></td><td>#fcdaeb</td><td>(252, 218, 235)</td></tr>
<tr><td>150</td><td><img src="https://placehold.co/15x15/f1f1f1/f1f1f1.png" alt="s"/></td><td>#f1f1f1</td><td>(241, 241, 241)</td></tr>
<tr><td>151</td><td><img src="https://placehold.co/15x15/cccccc/cccccc.png" alt="s"/></td><td>#cccccc</td><td>(204, 204, 204)</td></tr>
<tr><td>152</td><td><img src="https://placehold.co/15x15/f0e2cc/f0e2cc.png" alt="s"/></td><td>#f0e2cc</td><td>(240, 226, 204)</td></tr>
<tr><td>153</td><td><img src="https://placehold.co/15x15/fff1ae/fff1ae.png" alt="s"/></td><td>#fff1ae</td><td>(255, 241, 174)</td></tr>
<tr><td>154</td><td><img src="https://placehold.co/15x15/e6f4c9/e6f4c9.png" alt="s"/></td><td>#e6f4c9</td><td>(230, 244, 201)</td></tr>
<tr><td>155</td><td><img src="https://placehold.co/15x15/f3cae4/f3cae4.png" alt="s"/></td><td>#f3cae4</td><td>(243, 202, 228)</td></tr>
<tr><td>156</td><td><img src="https://placehold.co/15x15/cbd5e7/cbd5e7.png" alt="s"/></td><td>#cbd5e7</td><td>(203, 213, 231)</td></tr>
<tr><td>157</td><td><img src="https://placehold.co/15x15/fccdac/fccdac.png" alt="s"/></td><td>#fccdac</td><td>(252, 205, 172)</td></tr>
<tr><td>158</td><td><img src="https://placehold.co/15x15/b2e2cd/b2e2cd.png" alt="s"/></td><td>#b2e2cd</td><td>(178, 226, 205)</td></tr>
<tr><td>159</td><td><img src="https://placehold.co/15x15/a6cee3/a6cee3.png" alt="s"/></td><td>#a6cee3</td><td>(166, 206, 227)</td></tr>
<tr><td>160</td><td><img src="https://placehold.co/15x15/1e78b4/1e78b4.png" alt="s"/></td><td>#1e78b4</td><td>(30, 120, 180)</td></tr>
<tr><td>161</td><td><img src="https://placehold.co/15x15/b2df89/b2df89.png" alt="s"/></td><td>#b2df89</td><td>(178, 223, 137)</td></tr>
<tr><td>162</td><td><img src="https://placehold.co/15x15/33a02b/33a02b.png" alt="s"/></td><td>#33a02b</td><td>(51, 160, 43)</td></tr>
<tr><td>163</td><td><img src="https://placehold.co/15x15/fb9a99/fb9a99.png" alt="s"/></td><td>#fb9a99</td><td>(251, 154, 153)</td></tr>
<tr><td>164</td><td><img src="https://placehold.co/15x15/e3191b/e3191b.png" alt="s"/></td><td>#e3191b</td><td>(227, 25, 27)</td></tr>
<tr><td>165</td><td><img src="https://placehold.co/15x15/fcbe6f/fcbe6f.png" alt="s"/></td><td>#fcbe6f</td><td>(252, 190, 111)</td></tr>
<tr><td>166</td><td><img src="https://placehold.co/15x15/ff7f00/ff7f00.png" alt="s"/></td><td>#ff7f00</td><td>(255, 127, 0)</td></tr>
<tr><td>167</td><td><img src="https://placehold.co/15x15/cab2d6/cab2d6.png" alt="s"/></td><td>#cab2d6</td><td>(202, 178, 214)</td></tr>
<tr><td>168</td><td><img src="https://placehold.co/15x15/6a3d9a/6a3d9a.png" alt="s"/></td><td>#6a3d9a</td><td>(106, 61, 154)</td></tr>
<tr><td>169</td><td><img src="https://placehold.co/15x15/ffff99/ffff99.png" alt="s"/></td><td>#ffff99</td><td>(255, 255, 153)</td></tr>
<tr><td>170</td><td><img src="https://placehold.co/15x15/b15827/b15827.png" alt="s"/></td><td>#b15827</td><td>(177, 88, 39)</td></tr>
<tr><td>171</td><td><img src="https://placehold.co/15x15/7fc97f/7fc97f.png" alt="s"/></td><td>#7fc97f</td><td>(127, 201, 127)</td></tr>
<tr><td>172</td><td><img src="https://placehold.co/15x15/bdaed4/bdaed4.png" alt="s"/></td><td>#bdaed4</td><td>(189, 174, 212)</td></tr>
<tr><td>173</td><td><img src="https://placehold.co/15x15/fcbf85/fcbf85.png" alt="s"/></td><td>#fcbf85</td><td>(252, 191, 133)</td></tr>
<tr><td>174</td><td><img src="https://placehold.co/15x15/386cb0/386cb0.png" alt="s"/></td><td>#386cb0</td><td>(56, 108, 176)</td></tr>
<tr><td>175</td><td><img src="https://placehold.co/15x15/ef027f/ef027f.png" alt="s"/></td><td>#ef027f</td><td>(239, 2, 127)</td></tr>
<tr><td>176</td><td><img src="https://placehold.co/15x15/be5a16/be5a16.png" alt="s"/></td><td>#be5a16</td><td>(190, 90, 22)</td></tr>
<tr><td>177</td><td><img src="https://placehold.co/15x15/666666/666666.png" alt="s"/></td><td>#666666</td><td>(102, 102, 102)</td></tr>
<tr><td>178</td><td><img src="https://placehold.co/15x15/1a9e77/1a9e77.png" alt="s"/></td><td>#1a9e77</td><td>(26, 158, 119)</td></tr>
<tr><td>179</td><td><img src="https://placehold.co/15x15/d95e02/d95e02.png" alt="s"/></td><td>#d95e02</td><td>(217, 94, 2)</td></tr>
<tr><td>180</td><td><img src="https://placehold.co/15x15/7570b2/7570b2.png" alt="s"/></td><td>#7570b2</td><td>(117, 112, 178)</td></tr>
<tr><td>181</td><td><img src="https://placehold.co/15x15/e72889/e72889.png" alt="s"/></td><td>#e72889</td><td>(231, 40, 137)</td></tr>
<tr><td>182</td><td><img src="https://placehold.co/15x15/66a61d/66a61d.png" alt="s"/></td><td>#66a61d</td><td>(102, 166, 29)</td></tr>
<tr><td>183</td><td><img src="https://placehold.co/15x15/e6ab02/e6ab02.png" alt="s"/></td><td>#e6ab02</td><td>(230, 171, 2)</td></tr>
<tr><td>184</td><td><img src="https://placehold.co/15x15/a6761c/a6761c.png" alt="s"/></td><td>#a6761c</td><td>(166, 118, 28)</td></tr>
<tr><td>185</td><td><img src="https://placehold.co/15x15/e4191b/e4191b.png" alt="s"/></td><td>#e4191b</td><td>(228, 25, 27)</td></tr>
<tr><td>186</td><td><img src="https://placehold.co/15x15/377eb7/377eb7.png" alt="s"/></td><td>#377eb7</td><td>(55, 126, 183)</td></tr>
<tr><td>187</td><td><img src="https://placehold.co/15x15/4caf4a/4caf4a.png" alt="s"/></td><td>#4caf4a</td><td>(76, 175, 74)</td></tr>
<tr><td>188</td><td><img src="https://placehold.co/15x15/984ea3/984ea3.png" alt="s"/></td><td>#984ea3</td><td>(152, 78, 163)</td></tr>
<tr><td>189</td><td><img src="https://placehold.co/15x15/ffff33/ffff33.png" alt="s"/></td><td>#ffff33</td><td>(255, 255, 51)</td></tr>
<tr><td>190</td><td><img src="https://placehold.co/15x15/a65527/a65527.png" alt="s"/></td><td>#a65527</td><td>(166, 85, 39)</td></tr>
<tr><td>191</td><td><img src="https://placehold.co/15x15/f680be/f680be.png" alt="s"/></td><td>#f680be</td><td>(246, 128, 190)</td></tr>
<tr><td>192</td><td><img src="https://placehold.co/15x15/999999/999999.png" alt="s"/></td><td>#999999</td><td>(153, 153, 153)</td></tr>
<tr><td>193</td><td><img src="https://placehold.co/15x15/66c1a5/66c1a5.png" alt="s"/></td><td>#66c1a5</td><td>(102, 193, 165)</td></tr>
<tr><td>194</td><td><img src="https://placehold.co/15x15/fb8c61/fb8c61.png" alt="s"/></td><td>#fb8c61</td><td>(251, 140, 97)</td></tr>
<tr><td>195</td><td><img src="https://placehold.co/15x15/8ca0cb/8ca0cb.png" alt="s"/></td><td>#8ca0cb</td><td>(140, 160, 203)</td></tr>
<tr><td>196</td><td><img src="https://placehold.co/15x15/e789c2/e789c2.png" alt="s"/></td><td>#e789c2</td><td>(231, 137, 194)</td></tr>
<tr><td>197</td><td><img src="https://placehold.co/15x15/a6d853/a6d853.png" alt="s"/></td><td>#a6d853</td><td>(166, 216, 83)</td></tr>
<tr><td>198</td><td><img src="https://placehold.co/15x15/ffd92e/ffd92e.png" alt="s"/></td><td>#ffd92e</td><td>(255, 217, 46)</td></tr>
<tr><td>199</td><td><img src="https://placehold.co/15x15/e5c393/e5c393.png" alt="s"/></td><td>#e5c393</td><td>(229, 195, 147)</td></tr>
<tr><td>200</td><td><img src="https://placehold.co/15x15/b2b2b2/b2b2b2.png" alt="s"/></td><td>#b2b2b2</td><td>(178, 178, 178)</td></tr>
<tr><td>201</td><td><img src="https://placehold.co/15x15/8cd3c6/8cd3c6.png" alt="s"/></td><td>#8cd3c6</td><td>(140, 211, 198)</td></tr>
<tr><td>202</td><td><img src="https://placehold.co/15x15/ffffb2/ffffb2.png" alt="s"/></td><td>#ffffb2</td><td>(255, 255, 178)</td></tr>
<tr><td>203</td><td><img src="https://placehold.co/15x15/bdb9da/bdb9da.png" alt="s"/></td><td>#bdb9da</td><td>(189, 185, 218)</td></tr>
<tr><td>204</td><td><img src="https://placehold.co/15x15/fb8072/fb8072.png" alt="s"/></td><td>#fb8072</td><td>(251, 128, 114)</td></tr>
<tr><td>205</td><td><img src="https://placehold.co/15x15/80b1d3/80b1d3.png" alt="s"/></td><td>#80b1d3</td><td>(128, 177, 211)</td></tr>
<tr><td>206</td><td><img src="https://placehold.co/15x15/fcb461/fcb461.png" alt="s"/></td><td>#fcb461</td><td>(252, 180, 97)</td></tr>
<tr><td>207</td><td><img src="https://placehold.co/15x15/b2de69/b2de69.png" alt="s"/></td><td>#b2de69</td><td>(178, 222, 105)</td></tr>
<tr><td>208</td><td><img src="https://placehold.co/15x15/fbcde5/fbcde5.png" alt="s"/></td><td>#fbcde5</td><td>(251, 205, 229)</td></tr>
<tr><td>209</td><td><img src="https://placehold.co/15x15/d9d9d9/d9d9d9.png" alt="s"/></td><td>#d9d9d9</td><td>(217, 217, 217)</td></tr>
<tr><td>210</td><td><img src="https://placehold.co/15x15/bb80bc/bb80bc.png" alt="s"/></td><td>#bb80bc</td><td>(187, 128, 188)</td></tr>
<tr><td>211</td><td><img src="https://placehold.co/15x15/ffec6f/ffec6f.png" alt="s"/></td><td>#ffec6f</td><td>(255, 236, 111)</td></tr>
<tr><td>212</td><td><img src="https://placehold.co/15x15/1e77b4/1e77b4.png" alt="s"/></td><td>#1e77b4</td><td>(30, 119, 180)</td></tr>
<tr><td>213</td><td><img src="https://placehold.co/15x15/ff7f0d/ff7f0d.png" alt="s"/></td><td>#ff7f0d</td><td>(255, 127, 13)</td></tr>
<tr><td>214</td><td><img src="https://placehold.co/15x15/2ba02b/2ba02b.png" alt="s"/></td><td>#2ba02b</td><td>(43, 160, 43)</td></tr>
<tr><td>215</td><td><img src="https://placehold.co/15x15/d62627/d62627.png" alt="s"/></td><td>#d62627</td><td>(214, 38, 39)</td></tr>
<tr><td>216</td><td><img src="https://placehold.co/15x15/9367bc/9367bc.png" alt="s"/></td><td>#9367bc</td><td>(147, 103, 188)</td></tr>
<tr><td>217</td><td><img src="https://placehold.co/15x15/8b554b/8b554b.png" alt="s"/></td><td>#8b554b</td><td>(139, 85, 75)</td></tr>
<tr><td>218</td><td><img src="https://placehold.co/15x15/e377c1/e377c1.png" alt="s"/></td><td>#e377c1</td><td>(227, 119, 193)</td></tr>
<tr><td>219</td><td><img src="https://placehold.co/15x15/7f7f7f/7f7f7f.png" alt="s"/></td><td>#7f7f7f</td><td>(127, 127, 127)</td></tr>
<tr><td>220</td><td><img src="https://placehold.co/15x15/bbbc21/bbbc21.png" alt="s"/></td><td>#bbbc21</td><td>(187, 188, 33)</td></tr>
<tr><td>221</td><td><img src="https://placehold.co/15x15/17bdcf/17bdcf.png" alt="s"/></td><td>#17bdcf</td><td>(23, 189, 207)</td></tr>
<tr><td>222</td><td><img src="https://placehold.co/15x15/aec6e7/aec6e7.png" alt="s"/></td><td>#aec6e7</td><td>(174, 198, 231)</td></tr>
<tr><td>223</td><td><img src="https://placehold.co/15x15/ffba78/ffba78.png" alt="s"/></td><td>#ffba78</td><td>(255, 186, 120)</td></tr>
<tr><td>224</td><td><img src="https://placehold.co/15x15/98df89/98df89.png" alt="s"/></td><td>#98df89</td><td>(152, 223, 137)</td></tr>
<tr><td>225</td><td><img src="https://placehold.co/15x15/ff9895/ff9895.png" alt="s"/></td><td>#ff9895</td><td>(255, 152, 149)</td></tr>
<tr><td>226</td><td><img src="https://placehold.co/15x15/c4b0d5/c4b0d5.png" alt="s"/></td><td>#c4b0d5</td><td>(196, 176, 213)</td></tr>
<tr><td>227</td><td><img src="https://placehold.co/15x15/c39c93/c39c93.png" alt="s"/></td><td>#c39c93</td><td>(195, 156, 147)</td></tr>
<tr><td>228</td><td><img src="https://placehold.co/15x15/f6b5d2/f6b5d2.png" alt="s"/></td><td>#f6b5d2</td><td>(246, 181, 210)</td></tr>
<tr><td>229</td><td><img src="https://placehold.co/15x15/c6c6c6/c6c6c6.png" alt="s"/></td><td>#c6c6c6</td><td>(198, 198, 198)</td></tr>
<tr><td>230</td><td><img src="https://placehold.co/15x15/dbdb8c/dbdb8c.png" alt="s"/></td><td>#dbdb8c</td><td>(219, 219, 140)</td></tr>
<tr><td>231</td><td><img src="https://placehold.co/15x15/9edae5/9edae5.png" alt="s"/></td><td>#9edae5</td><td>(158, 218, 229)</td></tr>
<tr><td>232</td><td><img src="https://placehold.co/15x15/393b79/393b79.png" alt="s"/></td><td>#393b79</td><td>(57, 59, 121)</td></tr>
<tr><td>233</td><td><img src="https://placehold.co/15x15/5153a3/5153a3.png" alt="s"/></td><td>#5153a3</td><td>(81, 83, 163)</td></tr>
<tr><td>234</td><td><img src="https://placehold.co/15x15/6b6ecf/6b6ecf.png" alt="s"/></td><td>#6b6ecf</td><td>(107, 110, 207)</td></tr>
<tr><td>235</td><td><img src="https://placehold.co/15x15/9c9ede/9c9ede.png" alt="s"/></td><td>#9c9ede</td><td>(156, 158, 222)</td></tr>
<tr><td>236</td><td><img src="https://placehold.co/15x15/627939/627939.png" alt="s"/></td><td>#627939</td><td>(98, 121, 57)</td></tr>
<tr><td>237</td><td><img src="https://placehold.co/15x15/8ba251/8ba251.png" alt="s"/></td><td>#8ba251</td><td>(139, 162, 81)</td></tr>
<tr><td>238</td><td><img src="https://placehold.co/15x15/b5cf6b/b5cf6b.png" alt="s"/></td><td>#b5cf6b</td><td>(181, 207, 107)</td></tr>
<tr><td>239</td><td><img src="https://placehold.co/15x15/cedb9c/cedb9c.png" alt="s"/></td><td>#cedb9c</td><td>(206, 219, 156)</td></tr>
<tr><td>240</td><td><img src="https://placehold.co/15x15/8b6d30/8b6d30.png" alt="s"/></td><td>#8b6d30</td><td>(139, 109, 48)</td></tr>
<tr><td>241</td><td><img src="https://placehold.co/15x15/bc9e39/bc9e39.png" alt="s"/></td><td>#bc9e39</td><td>(188, 158, 57)</td></tr>
<tr><td>242</td><td><img src="https://placehold.co/15x15/e7b951/e7b951.png" alt="s"/></td><td>#e7b951</td><td>(231, 185, 81)</td></tr>
<tr><td>243</td><td><img src="https://placehold.co/15x15/e7cb93/e7cb93.png" alt="s"/></td><td>#e7cb93</td><td>(231, 203, 147)</td></tr>
<tr><td>244</td><td><img src="https://placehold.co/15x15/843c39/843c39.png" alt="s"/></td><td>#843c39</td><td>(132, 60, 57)</td></tr>
<tr><td>245</td><td><img src="https://placehold.co/15x15/ad494a/ad494a.png" alt="s"/></td><td>#ad494a</td><td>(173, 73, 74)</td></tr>
<tr><td>246</td><td><img src="https://placehold.co/15x15/d6606b/d6606b.png" alt="s"/></td><td>#d6606b</td><td>(214, 96, 107)</td></tr>
<tr><td>247</td><td><img src="https://placehold.co/15x15/e7959c/e7959c.png" alt="s"/></td><td>#e7959c</td><td>(231, 149, 156)</td></tr>
<tr><td>248</td><td><img src="https://placehold.co/15x15/7b4173/7b4173.png" alt="s"/></td><td>#7b4173</td><td>(123, 65, 115)</td></tr>
<tr><td>249</td><td><img src="https://placehold.co/15x15/a55093/a55093.png" alt="s"/></td><td>#a55093</td><td>(165, 80, 147)</td></tr>
<tr><td>250</td><td><img src="https://placehold.co/15x15/ce6dbc/ce6dbc.png" alt="s"/></td><td>#ce6dbc</td><td>(206, 109, 188)</td></tr>
<tr><td>251</td><td><img src="https://placehold.co/15x15/de9ed6/de9ed6.png" alt="s"/></td><td>#de9ed6</td><td>(222, 158, 214)</td></tr>
<tr><td>252</td><td><img src="https://placehold.co/15x15/3081bc/3081bc.png" alt="s"/></td><td>#3081bc</td><td>(48, 129, 188)</td></tr>
<tr><td>253</td><td><img src="https://placehold.co/15x15/6baed6/6baed6.png" alt="s"/></td><td>#6baed6</td><td>(107, 174, 214)</td></tr>
<tr><td>254</td><td><img src="https://placehold.co/15x15/9ecae1/9ecae1.png" alt="s"/></td><td>#9ecae1</td><td>(158, 202, 225)</td></tr>
<tr><td>255</td><td><img src="https://placehold.co/15x15/c5dbee/c5dbee.png" alt="s"/></td><td>#c5dbee</td><td>(197, 219, 238)</td></tr>
<tr><td>256</td><td><img src="https://placehold.co/15x15/e6540c/e6540c.png" alt="s"/></td><td>#e6540c</td><td>(230, 84, 12)</td></tr>
<tr><td>257</td><td><img src="https://placehold.co/15x15/fc8c3c/fc8c3c.png" alt="s"/></td><td>#fc8c3c</td><td>(252, 140, 60)</td></tr>
<tr><td>258</td><td><img src="https://placehold.co/15x15/fcae6b/fcae6b.png" alt="s"/></td><td>#fcae6b</td><td>(252, 174, 107)</td></tr>
<tr><td>259</td><td><img src="https://placehold.co/15x15/fcd0a2/fcd0a2.png" alt="s"/></td><td>#fcd0a2</td><td>(252, 208, 162)</td></tr>
<tr><td>260</td><td><img src="https://placehold.co/15x15/30a353/30a353.png" alt="s"/></td><td>#30a353</td><td>(48, 163, 83)</td></tr>
<tr><td>261</td><td><img src="https://placehold.co/15x15/74c376/74c376.png" alt="s"/></td><td>#74c376</td><td>(116, 195, 118)</td></tr>
<tr><td>262</td><td><img src="https://placehold.co/15x15/a1d99b/a1d99b.png" alt="s"/></td><td>#a1d99b</td><td>(161, 217, 155)</td></tr>
<tr><td>263</td><td><img src="https://placehold.co/15x15/c6e8bf/c6e8bf.png" alt="s"/></td><td>#c6e8bf</td><td>(198, 232, 191)</td></tr>
<tr><td>264</td><td><img src="https://placehold.co/15x15/756bb1/756bb1.png" alt="s"/></td><td>#756bb1</td><td>(117, 107, 177)</td></tr>
<tr><td>265</td><td><img src="https://placehold.co/15x15/9e9ac7/9e9ac7.png" alt="s"/></td><td>#9e9ac7</td><td>(158, 154, 199)</td></tr>
<tr><td>266</td><td><img src="https://placehold.co/15x15/bbbcdc/bbbcdc.png" alt="s"/></td><td>#bbbcdc</td><td>(187, 188, 220)</td></tr>
<tr><td>267</td><td><img src="https://placehold.co/15x15/dadaea/dadaea.png" alt="s"/></td><td>#dadaea</td><td>(218, 218, 234)</td></tr>
<tr><td>268</td><td><img src="https://placehold.co/15x15/626262/626262.png" alt="s"/></td><td>#626262</td><td>(98, 98, 98)</td></tr>
<tr><td>269</td><td><img src="https://placehold.co/15x15/959595/959595.png" alt="s"/></td><td>#959595</td><td>(149, 149, 149)</td></tr>
<tr><td>270</td><td><img src="https://placehold.co/15x15/bcbcbc/bcbcbc.png" alt="s"/></td><td>#bcbcbc</td><td>(188, 188, 188)</td></tr>
</table>