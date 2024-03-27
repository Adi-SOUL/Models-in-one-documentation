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
    ...  # Draw here, use default_painter instead of plt
    
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
</deflist>

`Models_in_one.utilis.painter`中索引与颜色对应如下表：

<table>
<tr><td>序号</td><td>颜色</td><td>HEX</td><td>RGB</td></tr>
<tr><td>1</td><td><format color="#000000" style="bold">███</format></td><td>#000000</td><td>(0, 0, 0)</td></tr>
<tr><td>2</td><td><format color="#8c8c8c" style="bold">███</format></td><td>#8c8c8c</td><td>(140, 140, 140)</td></tr>
<tr><td>3</td><td><format color="#a0a0a0" style="bold">███</format></td><td>#a0a0a0</td><td>(160, 160, 160)</td></tr>
<tr><td>4</td><td><format color="#c1c1c1" style="bold">███</format></td><td>#c1c1c1</td><td>(193, 193, 193)</td></tr>
<tr><td>5</td><td><format color="#d3d3d3" style="bold">███</format></td><td>#d3d3d3</td><td>(211, 211, 211)</td></tr>
<tr><td>6</td><td><format color="#e1e1e1" style="bold">███</format></td><td>#e1e1e1</td><td>(225, 225, 225)</td></tr>
<tr><td>7</td><td><format color="#e7e7e7" style="bold">███</format></td><td>#e7e7e7</td><td>(231, 231, 231)</td></tr>
<tr><td>8</td><td><format color="#f8f8f8" style="bold">███</format></td><td>#f8f8f8</td><td>(248, 248, 248)</td></tr>
<tr><td>9</td><td><format color="#fffafa" style="bold">███</format></td><td>#fffafa</td><td>(255, 250, 250)</td></tr>
<tr><td>10</td><td><format color="#bc8f8f" style="bold">███</format></td><td>#bc8f8f</td><td>(188, 143, 143)</td></tr>
<tr><td>11</td><td><format color="#f08080" style="bold">███</format></td><td>#f08080</td><td>(240, 128, 128)</td></tr>
<tr><td>12</td><td><format color="#cd5c5c" style="bold">███</format></td><td>#cd5c5c</td><td>(205, 92, 92)</td></tr>
<tr><td>13</td><td><format color="#a52a2a" style="bold">███</format></td><td>#a52a2a</td><td>(165, 42, 42)</td></tr>
<tr><td>14</td><td><format color="#b22222" style="bold">███</format></td><td>#b22222</td><td>(178, 34, 34)</td></tr>
<tr><td>15</td><td><format color="#800000" style="bold">███</format></td><td>#800000</td><td>(128, 0, 0)</td></tr>
<tr><td>16</td><td><format color="#8b0000" style="bold">███</format></td><td>#8b0000</td><td>(139, 0, 0)</td></tr>
<tr><td>17</td><td><format color="#ff0000" style="bold">███</format></td><td>#ff0000</td><td>(255, 0, 0)</td></tr>
<tr><td>18</td><td><format color="#ffe4e1" style="bold">███</format></td><td>#ffe4e1</td><td>(255, 228, 225)</td></tr>
<tr><td>19</td><td><format color="#fa8072" style="bold">███</format></td><td>#fa8072</td><td>(250, 128, 114)</td></tr>
<tr><td>20</td><td><format color="#ff6347" style="bold">███</format></td><td>#ff6347</td><td>(255, 99, 71)</td></tr>
<tr><td>21</td><td><format color="#e9967a" style="bold">███</format></td><td>#e9967a</td><td>(233, 150, 122)</td></tr>
<tr><td>22</td><td><format color="#ff7f50" style="bold">███</format></td><td>#ff7f50</td><td>(255, 127, 80)</td></tr>
<tr><td>23</td><td><format color="#ff4500" style="bold">███</format></td><td>#ff4500</td><td>(255, 69, 0)</td></tr>
<tr><td>24</td><td><format color="#ffa07a" style="bold">███</format></td><td>#ffa07a</td><td>(255, 160, 122)</td></tr>
<tr><td>25</td><td><format color="#a0522d" style="bold">███</format></td><td>#a0522d</td><td>(160, 82, 45)</td></tr>
<tr><td>26</td><td><format color="#fff5ee" style="bold">███</format></td><td>#fff5ee</td><td>(255, 245, 238)</td></tr>
<tr><td>27</td><td><format color="#d2691e" style="bold">███</format></td><td>#d2691e</td><td>(210, 105, 30)</td></tr>
<tr><td>28</td><td><format color="#8b4513" style="bold">███</format></td><td>#8b4513</td><td>(139, 69, 19)</td></tr>
<tr><td>29</td><td><format color="#f4a460" style="bold">███</format></td><td>#f4a460</td><td>(244, 164, 96)</td></tr>
<tr><td>30</td><td><format color="#ffdab9" style="bold">███</format></td><td>#ffdab9</td><td>(255, 218, 185)</td></tr>
<tr><td>31</td><td><format color="#cd853f" style="bold">███</format></td><td>#cd853f</td><td>(205, 133, 63)</td></tr>
<tr><td>32</td><td><format color="#faf0e6" style="bold">███</format></td><td>#faf0e6</td><td>(250, 240, 230)</td></tr>
<tr><td>33</td><td><format color="#ffe4c4" style="bold">███</format></td><td>#ffe4c4</td><td>(255, 228, 196)</td></tr>
<tr><td>34</td><td><format color="#ff8c00" style="bold">███</format></td><td>#ff8c00</td><td>(255, 140, 0)</td></tr>
<tr><td>35</td><td><format color="#deb887" style="bold">███</format></td><td>#deb887</td><td>(222, 184, 135)</td></tr>
<tr><td>36</td><td><format color="#faebd7" style="bold">███</format></td><td>#faebd7</td><td>(250, 235, 215)</td></tr>
<tr><td>37</td><td><format color="#d2b48c" style="bold">███</format></td><td>#d2b48c</td><td>(210, 180, 140)</td></tr>
<tr><td>38</td><td><format color="#ffdead" style="bold">███</format></td><td>#ffdead</td><td>(255, 222, 173)</td></tr>
<tr><td>39</td><td><format color="#ffebcd" style="bold">███</format></td><td>#ffebcd</td><td>(255, 235, 205)</td></tr>
<tr><td>40</td><td><format color="#ffefd5" style="bold">███</format></td><td>#ffefd5</td><td>(255, 239, 213)</td></tr>
<tr><td>41</td><td><format color="#ffe4b5" style="bold">███</format></td><td>#ffe4b5</td><td>(255, 228, 181)</td></tr>
<tr><td>42</td><td><format color="#ffa500" style="bold">███</format></td><td>#ffa500</td><td>(255, 165, 0)</td></tr>
<tr><td>43</td><td><format color="#f5deb3" style="bold">███</format></td><td>#f5deb3</td><td>(245, 222, 179)</td></tr>
<tr><td>44</td><td><format color="#fdf5e6" style="bold">███</format></td><td>#fdf5e6</td><td>(253, 245, 230)</td></tr>
<tr><td>45</td><td><format color="#fffaf0" style="bold">███</format></td><td>#fffaf0</td><td>(255, 250, 240)</td></tr>
<tr><td>46</td><td><format color="#b8860b" style="bold">███</format></td><td>#b8860b</td><td>(184, 134, 11)</td></tr>
<tr><td>47</td><td><format color="#daa520" style="bold">███</format></td><td>#daa520</td><td>(218, 165, 32)</td></tr>
<tr><td>48</td><td><format color="#fff8dc" style="bold">███</format></td><td>#fff8dc</td><td>(255, 248, 220)</td></tr>
<tr><td>49</td><td><format color="#ffd700" style="bold">███</format></td><td>#ffd700</td><td>(255, 215, 0)</td></tr>
<tr><td>50</td><td><format color="#fffacd" style="bold">███</format></td><td>#fffacd</td><td>(255, 250, 205)</td></tr>
<tr><td>51</td><td><format color="#f0e68c" style="bold">███</format></td><td>#f0e68c</td><td>(240, 230, 140)</td></tr>
<tr><td>52</td><td><format color="#eee8aa" style="bold">███</format></td><td>#eee8aa</td><td>(238, 232, 170)</td></tr>
<tr><td>53</td><td><format color="#bdb76b" style="bold">███</format></td><td>#bdb76b</td><td>(189, 183, 107)</td></tr>
<tr><td>54</td><td><format color="#fffff0" style="bold">███</format></td><td>#fffff0</td><td>(255, 255, 240)</td></tr>
<tr><td>55</td><td><format color="#f5f5dc" style="bold">███</format></td><td>#f5f5dc</td><td>(245, 245, 220)</td></tr>
<tr><td>56</td><td><format color="#ffffe0" style="bold">███</format></td><td>#ffffe0</td><td>(255, 255, 224)</td></tr>
<tr><td>57</td><td><format color="#fafad2" style="bold">███</format></td><td>#fafad2</td><td>(250, 250, 210)</td></tr>
<tr><td>58</td><td><format color="#808000" style="bold">███</format></td><td>#808000</td><td>(128, 128, 0)</td></tr>
<tr><td>59</td><td><format color="#bfbf00" style="bold">███</format></td><td>#bfbf00</td><td>(191, 191, 0)</td></tr>
<tr><td>60</td><td><format color="#ffff00" style="bold">███</format></td><td>#ffff00</td><td>(255, 255, 0)</td></tr>
<tr><td>61</td><td><format color="#6b8e23" style="bold">███</format></td><td>#6b8e23</td><td>(107, 142, 35)</td></tr>
<tr><td>62</td><td><format color="#9acd32" style="bold">███</format></td><td>#9acd32</td><td>(154, 205, 50)</td></tr>
<tr><td>63</td><td><format color="#556b2f" style="bold">███</format></td><td>#556b2f</td><td>(85, 107, 47)</td></tr>
<tr><td>64</td><td><format color="#adff2f" style="bold">███</format></td><td>#adff2f</td><td>(173, 255, 47)</td></tr>
<tr><td>65</td><td><format color="#7fff00" style="bold">███</format></td><td>#7fff00</td><td>(127, 255, 0)</td></tr>
<tr><td>66</td><td><format color="#7cfc00" style="bold">███</format></td><td>#7cfc00</td><td>(124, 252, 0)</td></tr>
<tr><td>67</td><td><format color="#f0fff0" style="bold">███</format></td><td>#f0fff0</td><td>(240, 255, 240)</td></tr>
<tr><td>68</td><td><format color="#8fbc8f" style="bold">███</format></td><td>#8fbc8f</td><td>(143, 188, 143)</td></tr>
<tr><td>69</td><td><format color="#98fb98" style="bold">███</format></td><td>#98fb98</td><td>(152, 251, 152)</td></tr>
<tr><td>70</td><td><format color="#90ee90" style="bold">███</format></td><td>#90ee90</td><td>(144, 238, 144)</td></tr>
<tr><td>71</td><td><format color="#228b22" style="bold">███</format></td><td>#228b22</td><td>(34, 139, 34)</td></tr>
<tr><td>72</td><td><format color="#32cd32" style="bold">███</format></td><td>#32cd32</td><td>(50, 205, 50)</td></tr>
<tr><td>73</td><td><format color="#006400" style="bold">███</format></td><td>#006400</td><td>(0, 100, 0)</td></tr>
<tr><td>74</td><td><format color="#008000" style="bold">███</format></td><td>#008000</td><td>(0, 128, 0)</td></tr>
<tr><td>75</td><td><format color="#00ff00" style="bold">███</format></td><td>#00ff00</td><td>(0, 255, 0)</td></tr>
<tr><td>76</td><td><format color="#2e8b57" style="bold">███</format></td><td>#2e8b57</td><td>(46, 139, 87)</td></tr>
<tr><td>77</td><td><format color="#3cb371" style="bold">███</format></td><td>#3cb371</td><td>(60, 179, 113)</td></tr>
<tr><td>78</td><td><format color="#00ff7f" style="bold">███</format></td><td>#00ff7f</td><td>(0, 255, 127)</td></tr>
<tr><td>79</td><td><format color="#f5fffa" style="bold">███</format></td><td>#f5fffa</td><td>(245, 255, 250)</td></tr>
<tr><td>80</td><td><format color="#00fa9a" style="bold">███</format></td><td>#00fa9a</td><td>(0, 250, 154)</td></tr>
<tr><td>81</td><td><format color="#66cdaa" style="bold">███</format></td><td>#66cdaa</td><td>(102, 205, 170)</td></tr>
<tr><td>82</td><td><format color="#7fffd4" style="bold">███</format></td><td>#7fffd4</td><td>(127, 255, 212)</td></tr>
<tr><td>83</td><td><format color="#40e0d0" style="bold">███</format></td><td>#40e0d0</td><td>(64, 224, 208)</td></tr>
<tr><td>84</td><td><format color="#20b2aa" style="bold">███</format></td><td>#20b2aa</td><td>(32, 178, 170)</td></tr>
<tr><td>85</td><td><format color="#48d1cc" style="bold">███</format></td><td>#48d1cc</td><td>(72, 209, 204)</td></tr>
<tr><td>86</td><td><format color="#f0ffff" style="bold">███</format></td><td>#f0ffff</td><td>(240, 255, 255)</td></tr>
<tr><td>87</td><td><format color="#e0ffff" style="bold">███</format></td><td>#e0ffff</td><td>(224, 255, 255)</td></tr>
<tr><td>88</td><td><format color="#afeeee" style="bold">███</format></td><td>#afeeee</td><td>(175, 238, 238)</td></tr>
<tr><td>89</td><td><format color="#2f4f4f" style="bold">███</format></td><td>#2f4f4f</td><td>(47, 79, 79)</td></tr>
<tr><td>90</td><td><format color="#008080" style="bold">███</format></td><td>#008080</td><td>(0, 128, 128)</td></tr>
<tr><td>91</td><td><format color="#008b8b" style="bold">███</format></td><td>#008b8b</td><td>(0, 139, 139)</td></tr>
<tr><td>92</td><td><format color="#00bfbf" style="bold">███</format></td><td>#00bfbf</td><td>(0, 191, 191)</td></tr>
<tr><td>93</td><td><format color="#00ffff" style="bold">███</format></td><td>#00ffff</td><td>(0, 255, 255)</td></tr>
<tr><td>94</td><td><format color="#00ced1" style="bold">███</format></td><td>#00ced1</td><td>(0, 206, 209)</td></tr>
<tr><td>95</td><td><format color="#5f9ea0" style="bold">███</format></td><td>#5f9ea0</td><td>(95, 158, 160)</td></tr>
<tr><td>96</td><td><format color="#b0e0e6" style="bold">███</format></td><td>#b0e0e6</td><td>(176, 224, 230)</td></tr>
<tr><td>97</td><td><format color="#add8e6" style="bold">███</format></td><td>#add8e6</td><td>(173, 216, 230)</td></tr>
<tr><td>98</td><td><format color="#00bfff" style="bold">███</format></td><td>#00bfff</td><td>(0, 191, 255)</td></tr>
<tr><td>99</td><td><format color="#87ceeb" style="bold">███</format></td><td>#87ceeb</td><td>(135, 206, 235)</td></tr>
<tr><td>100</td><td><format color="#87cefa" style="bold">███</format></td><td>#87cefa</td><td>(135, 206, 250)</td></tr>
<tr><td>101</td><td><format color="#4682b4" style="bold">███</format></td><td>#4682b4</td><td>(70, 130, 180)</td></tr>
<tr><td>102</td><td><format color="#f0f8ff" style="bold">███</format></td><td>#f0f8ff</td><td>(240, 248, 255)</td></tr>
<tr><td>103</td><td><format color="#1e90ff" style="bold">███</format></td><td>#1e90ff</td><td>(30, 144, 255)</td></tr>
<tr><td>104</td><td><format color="#778899" style="bold">███</format></td><td>#778899</td><td>(119, 136, 153)</td></tr>
<tr><td>105</td><td><format color="#708090" style="bold">███</format></td><td>#708090</td><td>(112, 128, 144)</td></tr>
<tr><td>106</td><td><format color="#b0c4de" style="bold">███</format></td><td>#b0c4de</td><td>(176, 196, 222)</td></tr>
<tr><td>107</td><td><format color="#6495ed" style="bold">███</format></td><td>#6495ed</td><td>(100, 149, 237)</td></tr>
<tr><td>108</td><td><format color="#4169e1" style="bold">███</format></td><td>#4169e1</td><td>(65, 105, 225)</td></tr>
<tr><td>109</td><td><format color="#f8f8ff" style="bold">███</format></td><td>#f8f8ff</td><td>(248, 248, 255)</td></tr>
<tr><td>110</td><td><format color="#e6e6fa" style="bold">███</format></td><td>#e6e6fa</td><td>(230, 230, 250)</td></tr>
<tr><td>111</td><td><format color="#191970" style="bold">███</format></td><td>#191970</td><td>(25, 25, 112)</td></tr>
<tr><td>112</td><td><format color="#000080" style="bold">███</format></td><td>#000080</td><td>(0, 0, 128)</td></tr>
<tr><td>113</td><td><format color="#00008b" style="bold">███</format></td><td>#00008b</td><td>(0, 0, 139)</td></tr>
<tr><td>114</td><td><format color="#0000cd" style="bold">███</format></td><td>#0000cd</td><td>(0, 0, 205)</td></tr>
<tr><td>115</td><td><format color="#0000ff" style="bold">███</format></td><td>#0000ff</td><td>(0, 0, 255)</td></tr>
<tr><td>116</td><td><format color="#6a5acd" style="bold">███</format></td><td>#6a5acd</td><td>(106, 90, 205)</td></tr>
<tr><td>117</td><td><format color="#483d8b" style="bold">███</format></td><td>#483d8b</td><td>(72, 61, 139)</td></tr>
<tr><td>118</td><td><format color="#7b68ee" style="bold">███</format></td><td>#7b68ee</td><td>(123, 104, 238)</td></tr>
<tr><td>119</td><td><format color="#9370db" style="bold">███</format></td><td>#9370db</td><td>(147, 112, 219)</td></tr>
<tr><td>120</td><td><format color="#663399" style="bold">███</format></td><td>#663399</td><td>(102, 51, 153)</td></tr>
<tr><td>121</td><td><format color="#8a2be2" style="bold">███</format></td><td>#8a2be2</td><td>(138, 43, 226)</td></tr>
<tr><td>122</td><td><format color="#4b0082" style="bold">███</format></td><td>#4b0082</td><td>(75, 0, 130)</td></tr>
<tr><td>123</td><td><format color="#9932cc" style="bold">███</format></td><td>#9932cc</td><td>(153, 50, 204)</td></tr>
<tr><td>124</td><td><format color="#9400d3" style="bold">███</format></td><td>#9400d3</td><td>(148, 0, 211)</td></tr>
<tr><td>125</td><td><format color="#ba55d3" style="bold">███</format></td><td>#ba55d3</td><td>(186, 85, 211)</td></tr>
<tr><td>126</td><td><format color="#d8bfd8" style="bold">███</format></td><td>#d8bfd8</td><td>(216, 191, 216)</td></tr>
<tr><td>127</td><td><format color="#dda0dd" style="bold">███</format></td><td>#dda0dd</td><td>(221, 160, 221)</td></tr>
<tr><td>128</td><td><format color="#ee82ee" style="bold">███</format></td><td>#ee82ee</td><td>(238, 130, 238)</td></tr>
<tr><td>129</td><td><format color="#800080" style="bold">███</format></td><td>#800080</td><td>(128, 0, 128)</td></tr>
<tr><td>130</td><td><format color="#8b008b" style="bold">███</format></td><td>#8b008b</td><td>(139, 0, 139)</td></tr>
<tr><td>131</td><td><format color="#bf00bf" style="bold">███</format></td><td>#bf00bf</td><td>(191, 0, 191)</td></tr>
<tr><td>132</td><td><format color="#ff00ff" style="bold">███</format></td><td>#ff00ff</td><td>(255, 0, 255)</td></tr>
<tr><td>133</td><td><format color="#da70d6" style="bold">███</format></td><td>#da70d6</td><td>(218, 112, 214)</td></tr>
<tr><td>134</td><td><format color="#c71585" style="bold">███</format></td><td>#c71585</td><td>(199, 21, 133)</td></tr>
<tr><td>135</td><td><format color="#ff1493" style="bold">███</format></td><td>#ff1493</td><td>(255, 20, 147)</td></tr>
<tr><td>136</td><td><format color="#ff69b4" style="bold">███</format></td><td>#ff69b4</td><td>(255, 105, 180)</td></tr>
<tr><td>137</td><td><format color="#fff0f5" style="bold">███</format></td><td>#fff0f5</td><td>(255, 240, 245)</td></tr>
<tr><td>138</td><td><format color="#db7093" style="bold">███</format></td><td>#db7093</td><td>(219, 112, 147)</td></tr>
<tr><td>139</td><td><format color="#dc143c" style="bold">███</format></td><td>#dc143c</td><td>(220, 20, 60)</td></tr>
<tr><td>140</td><td><format color="#ffc0cb" style="bold">███</format></td><td>#ffc0cb</td><td>(255, 192, 203)</td></tr>
<tr><td>141</td><td><format color="#ffb6c1" style="bold">███</format></td><td>#ffb6c1</td><td>(255, 182, 193)</td></tr>
<tr><td>142</td><td><format color="#fbb4ae" style="bold">███</format></td><td>#fbb4ae</td><td>(251, 180, 174)</td></tr>
<tr><td>143</td><td><format color="#b3cde3" style="bold">███</format></td><td>#b3cde3</td><td>(179, 205, 227)</td></tr>
<tr><td>144</td><td><format color="#ccebc5" style="bold">███</format></td><td>#ccebc5</td><td>(204, 235, 197)</td></tr>
<tr><td>145</td><td><format color="#decbe4" style="bold">███</format></td><td>#decbe4</td><td>(222, 203, 228)</td></tr>
<tr><td>146</td><td><format color="#fed9a6" style="bold">███</format></td><td>#fed9a6</td><td>(254, 217, 166)</td></tr>
<tr><td>147</td><td><format color="#ffffcc" style="bold">███</format></td><td>#ffffcc</td><td>(255, 255, 204)</td></tr>
<tr><td>148</td><td><format color="#e5d8bd" style="bold">███</format></td><td>#e5d8bd</td><td>(229, 216, 189)</td></tr>
<tr><td>149</td><td><format color="#fddaec" style="bold">███</format></td><td>#fddaec</td><td>(253, 218, 236)</td></tr>
<tr><td>150</td><td><format color="#f2f2f2" style="bold">███</format></td><td>#f2f2f2</td><td>(242, 242, 242)</td></tr>
<tr><td>151</td><td><format color="#cccccc" style="bold">███</format></td><td>#cccccc</td><td>(204, 204, 204)</td></tr>
<tr><td>152</td><td><format color="#f1e2cc" style="bold">███</format></td><td>#f1e2cc</td><td>(241, 226, 204)</td></tr>
<tr><td>153</td><td><format color="#fff2ae" style="bold">███</format></td><td>#fff2ae</td><td>(255, 242, 174)</td></tr>
<tr><td>154</td><td><format color="#e6f5c9" style="bold">███</format></td><td>#e6f5c9</td><td>(230, 245, 201)</td></tr>
<tr><td>155</td><td><format color="#f4cae4" style="bold">███</format></td><td>#f4cae4</td><td>(244, 202, 228)</td></tr>
<tr><td>156</td><td><format color="#cbd5e8" style="bold">███</format></td><td>#cbd5e8</td><td>(203, 213, 232)</td></tr>
<tr><td>157</td><td><format color="#fdcdac" style="bold">███</format></td><td>#fdcdac</td><td>(253, 205, 172)</td></tr>
<tr><td>158</td><td><format color="#b3e2cd" style="bold">███</format></td><td>#b3e2cd</td><td>(179, 226, 205)</td></tr>
<tr><td>159</td><td><format color="#a6cee3" style="bold">███</format></td><td>#a6cee3</td><td>(166, 206, 227)</td></tr>
<tr><td>160</td><td><format color="#1f78b4" style="bold">███</format></td><td>#1f78b4</td><td>(31, 120, 180)</td></tr>
<tr><td>161</td><td><format color="#b2df8a" style="bold">███</format></td><td>#b2df8a</td><td>(178, 223, 138)</td></tr>
<tr><td>162</td><td><format color="#33a02c" style="bold">███</format></td><td>#33a02c</td><td>(51, 160, 44)</td></tr>
<tr><td>163</td><td><format color="#fb9a99" style="bold">███</format></td><td>#fb9a99</td><td>(251, 154, 153)</td></tr>
<tr><td>164</td><td><format color="#e31a1c" style="bold">███</format></td><td>#e31a1c</td><td>(227, 26, 28)</td></tr>
<tr><td>165</td><td><format color="#fdbf6f" style="bold">███</format></td><td>#fdbf6f</td><td>(253, 191, 111)</td></tr>
<tr><td>166</td><td><format color="#ff7f00" style="bold">███</format></td><td>#ff7f00</td><td>(255, 127, 0)</td></tr>
<tr><td>167</td><td><format color="#cab2d6" style="bold">███</format></td><td>#cab2d6</td><td>(202, 178, 214)</td></tr>
<tr><td>168</td><td><format color="#6a3d9a" style="bold">███</format></td><td>#6a3d9a</td><td>(106, 61, 154)</td></tr>
<tr><td>169</td><td><format color="#ffff99" style="bold">███</format></td><td>#ffff99</td><td>(255, 255, 153)</td></tr>
<tr><td>170</td><td><format color="#b15928" style="bold">███</format></td><td>#b15928</td><td>(177, 89, 40)</td></tr>
<tr><td>171</td><td><format color="#7fc97f" style="bold">███</format></td><td>#7fc97f</td><td>(127, 201, 127)</td></tr>
<tr><td>172</td><td><format color="#beaed4" style="bold">███</format></td><td>#beaed4</td><td>(190, 174, 212)</td></tr>
<tr><td>173</td><td><format color="#fdc086" style="bold">███</format></td><td>#fdc086</td><td>(253, 192, 134)</td></tr>
<tr><td>174</td><td><format color="#386cb0" style="bold">███</format></td><td>#386cb0</td><td>(56, 108, 176)</td></tr>
<tr><td>175</td><td><format color="#f0027f" style="bold">███</format></td><td>#f0027f</td><td>(240, 2, 127)</td></tr>
<tr><td>176</td><td><format color="#bf5b16" style="bold">███</format></td><td>#bf5b16</td><td>(191, 91, 22)</td></tr>
<tr><td>177</td><td><format color="#666666" style="bold">███</format></td><td>#666666</td><td>(102, 102, 102)</td></tr>
<tr><td>178</td><td><format color="#1b9e77" style="bold">███</format></td><td>#1b9e77</td><td>(27, 158, 119)</td></tr>
<tr><td>179</td><td><format color="#d95f02" style="bold">███</format></td><td>#d95f02</td><td>(217, 95, 2)</td></tr>
<tr><td>180</td><td><format color="#7570b3" style="bold">███</format></td><td>#7570b3</td><td>(117, 112, 179)</td></tr>
<tr><td>181</td><td><format color="#e7298a" style="bold">███</format></td><td>#e7298a</td><td>(231, 41, 138)</td></tr>
<tr><td>182</td><td><format color="#66a61e" style="bold">███</format></td><td>#66a61e</td><td>(102, 166, 30)</td></tr>
<tr><td>183</td><td><format color="#e6ab02" style="bold">███</format></td><td>#e6ab02</td><td>(230, 171, 2)</td></tr>
<tr><td>184</td><td><format color="#a6761d" style="bold">███</format></td><td>#a6761d</td><td>(166, 118, 29)</td></tr>
<tr><td>185</td><td><format color="#e41a1c" style="bold">███</format></td><td>#e41a1c</td><td>(228, 26, 28)</td></tr>
<tr><td>186</td><td><format color="#377eb8" style="bold">███</format></td><td>#377eb8</td><td>(55, 126, 184)</td></tr>
<tr><td>187</td><td><format color="#4daf4a" style="bold">███</format></td><td>#4daf4a</td><td>(77, 175, 74)</td></tr>
<tr><td>188</td><td><format color="#984ea3" style="bold">███</format></td><td>#984ea3</td><td>(152, 78, 163)</td></tr>
<tr><td>189</td><td><format color="#ffff33" style="bold">███</format></td><td>#ffff33</td><td>(255, 255, 51)</td></tr>
<tr><td>190</td><td><format color="#a65628" style="bold">███</format></td><td>#a65628</td><td>(166, 86, 40)</td></tr>
<tr><td>191</td><td><format color="#f781bf" style="bold">███</format></td><td>#f781bf</td><td>(247, 129, 191)</td></tr>
<tr><td>192</td><td><format color="#999999" style="bold">███</format></td><td>#999999</td><td>(153, 153, 153)</td></tr>
<tr><td>193</td><td><format color="#66c2a5" style="bold">███</format></td><td>#66c2a5</td><td>(102, 194, 165)</td></tr>
<tr><td>194</td><td><format color="#fc8d62" style="bold">███</format></td><td>#fc8d62</td><td>(252, 141, 98)</td></tr>
<tr><td>195</td><td><format color="#8da0cb" style="bold">███</format></td><td>#8da0cb</td><td>(141, 160, 203)</td></tr>
<tr><td>196</td><td><format color="#e78ac3" style="bold">███</format></td><td>#e78ac3</td><td>(231, 138, 195)</td></tr>
<tr><td>197</td><td><format color="#a6d854" style="bold">███</format></td><td>#a6d854</td><td>(166, 216, 84)</td></tr>
<tr><td>198</td><td><format color="#ffd92f" style="bold">███</format></td><td>#ffd92f</td><td>(255, 217, 47)</td></tr>
<tr><td>199</td><td><format color="#e5c494" style="bold">███</format></td><td>#e5c494</td><td>(229, 196, 148)</td></tr>
<tr><td>200</td><td><format color="#b3b3b3" style="bold">███</format></td><td>#b3b3b3</td><td>(179, 179, 179)</td></tr>
<tr><td>201</td><td><format color="#8dd3c7" style="bold">███</format></td><td>#8dd3c7</td><td>(141, 211, 199)</td></tr>
<tr><td>202</td><td><format color="#ffffb3" style="bold">███</format></td><td>#ffffb3</td><td>(255, 255, 179)</td></tr>
<tr><td>203</td><td><format color="#bebada" style="bold">███</format></td><td>#bebada</td><td>(190, 186, 218)</td></tr>
<tr><td>204</td><td><format color="#fb8072" style="bold">███</format></td><td>#fb8072</td><td>(251, 128, 114)</td></tr>
<tr><td>205</td><td><format color="#80b1d3" style="bold">███</format></td><td>#80b1d3</td><td>(128, 177, 211)</td></tr>
<tr><td>206</td><td><format color="#fdb462" style="bold">███</format></td><td>#fdb462</td><td>(253, 180, 98)</td></tr>
<tr><td>207</td><td><format color="#b3de69" style="bold">███</format></td><td>#b3de69</td><td>(179, 222, 105)</td></tr>
<tr><td>208</td><td><format color="#fccde5" style="bold">███</format></td><td>#fccde5</td><td>(252, 205, 229)</td></tr>
<tr><td>209</td><td><format color="#d9d9d9" style="bold">███</format></td><td>#d9d9d9</td><td>(217, 217, 217)</td></tr>
<tr><td>210</td><td><format color="#bc80bd" style="bold">███</format></td><td>#bc80bd</td><td>(188, 128, 189)</td></tr>
<tr><td>211</td><td><format color="#ffed6f" style="bold">███</format></td><td>#ffed6f</td><td>(255, 237, 111)</td></tr>
<tr><td>212</td><td><format color="#1f77b4" style="bold">███</format></td><td>#1f77b4</td><td>(31, 119, 180)</td></tr>
<tr><td>213</td><td><format color="#ff7f0e" style="bold">███</format></td><td>#ff7f0e</td><td>(255, 127, 14)</td></tr>
<tr><td>214</td><td><format color="#2ca02c" style="bold">███</format></td><td>#2ca02c</td><td>(44, 160, 44)</td></tr>
<tr><td>215</td><td><format color="#d62728" style="bold">███</format></td><td>#d62728</td><td>(214, 39, 40)</td></tr>
<tr><td>216</td><td><format color="#9467bd" style="bold">███</format></td><td>#9467bd</td><td>(148, 103, 189)</td></tr>
<tr><td>217</td><td><format color="#8c564b" style="bold">███</format></td><td>#8c564b</td><td>(140, 86, 75)</td></tr>
<tr><td>218</td><td><format color="#e377c2" style="bold">███</format></td><td>#e377c2</td><td>(227, 119, 194)</td></tr>
<tr><td>219</td><td><format color="#7f7f7f" style="bold">███</format></td><td>#7f7f7f</td><td>(127, 127, 127)</td></tr>
<tr><td>220</td><td><format color="#bcbd22" style="bold">███</format></td><td>#bcbd22</td><td>(188, 189, 34)</td></tr>
<tr><td>221</td><td><format color="#17becf" style="bold">███</format></td><td>#17becf</td><td>(23, 190, 207)</td></tr>
<tr><td>222</td><td><format color="#aec7e8" style="bold">███</format></td><td>#aec7e8</td><td>(174, 199, 232)</td></tr>
<tr><td>223</td><td><format color="#ffbb78" style="bold">███</format></td><td>#ffbb78</td><td>(255, 187, 120)</td></tr>
<tr><td>224</td><td><format color="#98df8a" style="bold">███</format></td><td>#98df8a</td><td>(152, 223, 138)</td></tr>
<tr><td>225</td><td><format color="#ff9896" style="bold">███</format></td><td>#ff9896</td><td>(255, 152, 150)</td></tr>
<tr><td>226</td><td><format color="#c5b0d5" style="bold">███</format></td><td>#c5b0d5</td><td>(197, 176, 213)</td></tr>
<tr><td>227</td><td><format color="#c49c94" style="bold">███</format></td><td>#c49c94</td><td>(196, 156, 148)</td></tr>
<tr><td>228</td><td><format color="#f7b6d2" style="bold">███</format></td><td>#f7b6d2</td><td>(247, 182, 210)</td></tr>
<tr><td>229</td><td><format color="#c7c7c7" style="bold">███</format></td><td>#c7c7c7</td><td>(199, 199, 199)</td></tr>
<tr><td>230</td><td><format color="#dbdb8d" style="bold">███</format></td><td>#dbdb8d</td><td>(219, 219, 141)</td></tr>
<tr><td>231</td><td><format color="#9edae5" style="bold">███</format></td><td>#9edae5</td><td>(158, 218, 229)</td></tr>
<tr><td>232</td><td><format color="#393b79" style="bold">███</format></td><td>#393b79</td><td>(57, 59, 121)</td></tr>
<tr><td>233</td><td><format color="#5254a3" style="bold">███</format></td><td>#5254a3</td><td>(82, 84, 163)</td></tr>
<tr><td>234</td><td><format color="#6b6ecf" style="bold">███</format></td><td>#6b6ecf</td><td>(107, 110, 207)</td></tr>
<tr><td>235</td><td><format color="#9c9ede" style="bold">███</format></td><td>#9c9ede</td><td>(156, 158, 222)</td></tr>
<tr><td>236</td><td><format color="#637939" style="bold">███</format></td><td>#637939</td><td>(99, 121, 57)</td></tr>
<tr><td>237</td><td><format color="#8ca252" style="bold">███</format></td><td>#8ca252</td><td>(140, 162, 82)</td></tr>
<tr><td>238</td><td><format color="#b5cf6b" style="bold">███</format></td><td>#b5cf6b</td><td>(181, 207, 107)</td></tr>
<tr><td>239</td><td><format color="#cedb9c" style="bold">███</format></td><td>#cedb9c</td><td>(206, 219, 156)</td></tr>
<tr><td>240</td><td><format color="#8c6d31" style="bold">███</format></td><td>#8c6d31</td><td>(140, 109, 49)</td></tr>
<tr><td>241</td><td><format color="#bd9e39" style="bold">███</format></td><td>#bd9e39</td><td>(189, 158, 57)</td></tr>
<tr><td>242</td><td><format color="#e7ba52" style="bold">███</format></td><td>#e7ba52</td><td>(231, 186, 82)</td></tr>
<tr><td>243</td><td><format color="#e7cb94" style="bold">███</format></td><td>#e7cb94</td><td>(231, 203, 148)</td></tr>
<tr><td>244</td><td><format color="#843c39" style="bold">███</format></td><td>#843c39</td><td>(132, 60, 57)</td></tr>
<tr><td>245</td><td><format color="#ad494a" style="bold">███</format></td><td>#ad494a</td><td>(173, 73, 74)</td></tr>
<tr><td>246</td><td><format color="#d6616b" style="bold">███</format></td><td>#d6616b</td><td>(214, 97, 107)</td></tr>
<tr><td>247</td><td><format color="#e7969c" style="bold">███</format></td><td>#e7969c</td><td>(231, 150, 156)</td></tr>
<tr><td>248</td><td><format color="#7b4173" style="bold">███</format></td><td>#7b4173</td><td>(123, 65, 115)</td></tr>
<tr><td>249</td><td><format color="#a55194" style="bold">███</format></td><td>#a55194</td><td>(165, 81, 148)</td></tr>
<tr><td>250</td><td><format color="#ce6dbd" style="bold">███</format></td><td>#ce6dbd</td><td>(206, 109, 189)</td></tr>
<tr><td>251</td><td><format color="#de9ed6" style="bold">███</format></td><td>#de9ed6</td><td>(222, 158, 214)</td></tr>
<tr><td>252</td><td><format color="#3182bd" style="bold">███</format></td><td>#3182bd</td><td>(49, 130, 189)</td></tr>
<tr><td>253</td><td><format color="#6baed6" style="bold">███</format></td><td>#6baed6</td><td>(107, 174, 214)</td></tr>
<tr><td>254</td><td><format color="#9ecae1" style="bold">███</format></td><td>#9ecae1</td><td>(158, 202, 225)</td></tr>
<tr><td>255</td><td><format color="#c6dbef" style="bold">███</format></td><td>#c6dbef</td><td>(198, 219, 239)</td></tr>
<tr><td>256</td><td><format color="#e6550d" style="bold">███</format></td><td>#e6550d</td><td>(230, 85, 13)</td></tr>
<tr><td>257</td><td><format color="#fd8d3c" style="bold">███</format></td><td>#fd8d3c</td><td>(253, 141, 60)</td></tr>
<tr><td>258</td><td><format color="#fdae6b" style="bold">███</format></td><td>#fdae6b</td><td>(253, 174, 107)</td></tr>
<tr><td>259</td><td><format color="#fdd0a2" style="bold">███</format></td><td>#fdd0a2</td><td>(253, 208, 162)</td></tr>
<tr><td>260</td><td><format color="#31a354" style="bold">███</format></td><td>#31a354</td><td>(49, 163, 84)</td></tr>
<tr><td>261</td><td><format color="#74c476" style="bold">███</format></td><td>#74c476</td><td>(116, 196, 118)</td></tr>
<tr><td>262</td><td><format color="#a1d99b" style="bold">███</format></td><td>#a1d99b</td><td>(161, 217, 155)</td></tr>
<tr><td>263</td><td><format color="#c7e9c0" style="bold">███</format></td><td>#c7e9c0</td><td>(199, 233, 192)</td></tr>
<tr><td>264</td><td><format color="#756bb1" style="bold">███</format></td><td>#756bb1</td><td>(117, 107, 177)</td></tr>
<tr><td>265</td><td><format color="#9e9ac8" style="bold">███</format></td><td>#9e9ac8</td><td>(158, 154, 200)</td></tr>
<tr><td>266</td><td><format color="#bcbddc" style="bold">███</format></td><td>#bcbddc</td><td>(188, 189, 220)</td></tr>
<tr><td>267</td><td><format color="#dadaeb" style="bold">███</format></td><td>#dadaeb</td><td>(218, 218, 235)</td></tr>
<tr><td>268</td><td><format color="#636363" style="bold">███</format></td><td>#636363</td><td>(99, 99, 99)</td></tr>
<tr><td>269</td><td><format color="#969696" style="bold">███</format></td><td>#969696</td><td>(150, 150, 150)</td></tr>
<tr><td>270</td><td><format color="#bdbdbd" style="bold">███</format></td><td>#bdbdbd</td><td>(189, 189, 189)</td></tr>
</table>