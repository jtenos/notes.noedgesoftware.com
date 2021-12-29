---
layout: home
---

<pre style='color:#000000;background:#ffffff;'><span style='color:#800000; font-weight:bold; '>using</span> System<span style='color:#800080; '>;</span>
<span style='color:#800000; font-weight:bold; '>using</span> System<span style='color:#808030; '>.</span>Text<span style='color:#800080; '>;</span>
<span style='color:#800000; font-weight:bold; '>using</span> System<span style='color:#808030; '>.</span>IO<span style='color:#800080; '>;</span>

namespace Fesersoft<span style='color:#808030; '>.</span>Hashing
<span style='color:#800080; '>{</span>
    <span style='color:#3f5fbf; '>/// &lt;summary> </span>
    <span style='color:#3f5fbf; '>/// Get the CRC-32 Value for a String, Byte array or Stream </span>
    <span style='color:#3f5fbf; '>/// &lt;/summary> </span>
    public class crc32
    <span style='color:#696969; '>//  CRC32 Calculation on Strings, Byte arrays and Stream objects for .Net  </span>
    <span style='color:#696969; '>//  Released to the public domain with the following  </span>
    <span style='color:#696969; '>//  restrictions: </span>
    <span style='color:#696969; '>//   </span>
    <span style='color:#696969; '>//  1.  You may not modify the namespace. </span>
    <span style='color:#696969; '>//  2.  Your software must include acknowledgement that portions of the code are provided </span>
    <span style='color:#696969; '>//      by Fesersoft, Inc. </span>
    <span style='color:#696969; '>// </span>
    <span style='color:#696969; '>//  Copyright © 2001-2002 Fesersoft, Inc.  All Rights Reserved. </span>
    <span style='color:#696969; '>//  </span><span style='color:#5555dd; '>http://www.fesersoft.com/dotNet</span><span style='color:#696969; '> for updates and other software. </span>
    <span style='color:#800080; '>{</span>
        <span style='color:#3f5fbf; '>/// &lt;summary> </span>
        <span style='color:#3f5fbf; '>/// Create a new instance of the crc32 assembly. </span>
        <span style='color:#3f5fbf; '>/// &lt;/summary> </span>
        public crc32<span style='color:#808030; '>(</span><span style='color:#808030; '>)</span>
        <span style='color:#800080; '>{</span>
            <span style='color:#696969; '>// </span>
            <span style='color:#696969; '>// </span><span style='color:#ffffff; background:#808000; '>TODO: Add constructor logic here </span>
            <span style='color:#696969; '>// </span>
        <span style='color:#800080; '>}</span>

        readonly <span style='color:#800000; font-weight:bold; '>static</span> ulong<span style='color:#808030; '>[</span><span style='color:#808030; '>]</span> crcLookup <span style='color:#808030; '>=</span> new ulong<span style='color:#808030; '>[</span><span style='color:#808030; '>]</span> <span style='color:#800080; '>{</span> 
<span style='color:#008000; '>0x00000000</span><span style='color:#808030; '>,</span> <span style='color:#008000; '>0x77073096</span><span style='color:#808030; '>,</span> <span style='color:#008000; '>0xEE0E612C</span><span style='color:#808030; '>,</span> <span style='color:#008000; '>0x990951BA</span><span style='color:#808030; '>,</span> 
<span style='color:#008000; '>0x076DC419</span><span style='color:#808030; '>,</span> <span style='color:#008000; '>0x706AF48F</span><span style='color:#808030; '>,</span> <span style='color:#008000; '>0xE963A535</span><span style='color:#808030; '>,</span> <span style='color:#008000; '>0x9E6495A3</span><span style='color:#808030; '>,</span> 
<span style='color:#008000; '>0x0EDB8832</span><span style='color:#808030; '>,</span> <span style='color:#008000; '>0x79DCB8A4</span><span style='color:#808030; '>,</span> <span style='color:#008000; '>0xE0D5E91E</span><span style='color:#808030; '>,</span> <span style='color:#008000; '>0x97D2D988</span><span style='color:#808030; '>,</span> 
<span style='color:#008000; '>0x09B64C2B</span><span style='color:#808030; '>,</span> <span style='color:#008000; '>0x7EB17CBD</span><span style='color:#808030; '>,</span> <span style='color:#008000; '>0xE7B82D07</span><span style='color:#808030; '>,</span> <span style='color:#008000; '>0x90BF1D91</span><span style='color:#808030; '>,</span> 
<span style='color:#008000; '>0x1DB71064</span><span style='color:#808030; '>,</span> <span style='color:#008000; '>0x6AB020F2</span><span style='color:#808030; '>,</span> <span style='color:#008000; '>0xF3B97148</span><span style='color:#808030; '>,</span> <span style='color:#008000; '>0x84BE41DE</span><span style='color:#808030; '>,</span> 
<span style='color:#008000; '>0x1ADAD47D</span><span style='color:#808030; '>,</span> <span style='color:#008000; '>0x6DDDE4EB</span><span style='color:#808030; '>,</span> <span style='color:#008000; '>0xF4D4B551</span><span style='color:#808030; '>,</span> <span style='color:#008000; '>0x83D385C7</span><span style='color:#808030; '>,</span> 
<span style='color:#008000; '>0x136C9856</span><span style='color:#808030; '>,</span> <span style='color:#008000; '>0x646BA8C0</span><span style='color:#808030; '>,</span> <span style='color:#008000; '>0xFD62F97A</span><span style='color:#808030; '>,</span> <span style='color:#008000; '>0x8A65C9EC</span><span style='color:#808030; '>,</span> 
<span style='color:#008000; '>0x14015C4F</span><span style='color:#808030; '>,</span> <span style='color:#008000; '>0x63066CD9</span><span style='color:#808030; '>,</span> <span style='color:#008000; '>0xFA0F3D63</span><span style='color:#808030; '>,</span> <span style='color:#008000; '>0x8D080DF5</span><span style='color:#808030; '>,</span> 
<span style='color:#008000; '>0x3B6E20C8</span><span style='color:#808030; '>,</span> <span style='color:#008000; '>0x4C69105E</span><span style='color:#808030; '>,</span> <span style='color:#008000; '>0xD56041E4</span><span style='color:#808030; '>,</span> <span style='color:#008000; '>0xA2677172</span><span style='color:#808030; '>,</span> 
<span style='color:#008000; '>0x3C03E4D1</span><span style='color:#808030; '>,</span> <span style='color:#008000; '>0x4B04D447</span><span style='color:#808030; '>,</span> <span style='color:#008000; '>0xD20D85FD</span><span style='color:#808030; '>,</span> <span style='color:#008000; '>0xA50AB56B</span><span style='color:#808030; '>,</span> 
<span style='color:#008000; '>0x35B5A8FA</span><span style='color:#808030; '>,</span> <span style='color:#008000; '>0x42B2986C</span><span style='color:#808030; '>,</span> <span style='color:#008000; '>0xDBBBC9D6</span><span style='color:#808030; '>,</span> <span style='color:#008000; '>0xACBCF940</span><span style='color:#808030; '>,</span> 
<span style='color:#008000; '>0x32D86CE3</span><span style='color:#808030; '>,</span> <span style='color:#008000; '>0x45DF5C75</span><span style='color:#808030; '>,</span> <span style='color:#008000; '>0xDCD60DCF</span><span style='color:#808030; '>,</span> <span style='color:#008000; '>0xABD13D59</span><span style='color:#808030; '>,</span> 
<span style='color:#008000; '>0x26D930AC</span><span style='color:#808030; '>,</span> <span style='color:#008000; '>0x51DE003A</span><span style='color:#808030; '>,</span> <span style='color:#008000; '>0xC8D75180</span><span style='color:#808030; '>,</span> <span style='color:#008000; '>0xBFD06116</span><span style='color:#808030; '>,</span> 
<span style='color:#008000; '>0x21B4F4B5</span><span style='color:#808030; '>,</span> <span style='color:#008000; '>0x56B3C423</span><span style='color:#808030; '>,</span> <span style='color:#008000; '>0xCFBA9599</span><span style='color:#808030; '>,</span> <span style='color:#008000; '>0xB8BDA50F</span><span style='color:#808030; '>,</span> 
<span style='color:#008000; '>0x2802B89E</span><span style='color:#808030; '>,</span> <span style='color:#008000; '>0x5F058808</span><span style='color:#808030; '>,</span> <span style='color:#008000; '>0xC60CD9B2</span><span style='color:#808030; '>,</span> <span style='color:#008000; '>0xB10BE924</span><span style='color:#808030; '>,</span> 
<span style='color:#008000; '>0x2F6F7C87</span><span style='color:#808030; '>,</span> <span style='color:#008000; '>0x58684C11</span><span style='color:#808030; '>,</span> <span style='color:#008000; '>0xC1611DAB</span><span style='color:#808030; '>,</span> <span style='color:#008000; '>0xB6662D3D</span><span style='color:#808030; '>,</span> 
 
<span style='color:#008000; '>0x76DC4190</span><span style='color:#808030; '>,</span> <span style='color:#008000; '>0x01DB7106</span><span style='color:#808030; '>,</span> <span style='color:#008000; '>0x98D220BC</span><span style='color:#808030; '>,</span> <span style='color:#008000; '>0xEFD5102A</span><span style='color:#808030; '>,</span> 
<span style='color:#008000; '>0x71B18589</span><span style='color:#808030; '>,</span> <span style='color:#008000; '>0x06B6B51F</span><span style='color:#808030; '>,</span> <span style='color:#008000; '>0x9FBFE4A5</span><span style='color:#808030; '>,</span> <span style='color:#008000; '>0xE8B8D433</span><span style='color:#808030; '>,</span> 
<span style='color:#008000; '>0x7807C9A2</span><span style='color:#808030; '>,</span> <span style='color:#008000; '>0x0F00F934</span><span style='color:#808030; '>,</span> <span style='color:#008000; '>0x9609A88E</span><span style='color:#808030; '>,</span> <span style='color:#008000; '>0xE10E9818</span><span style='color:#808030; '>,</span> 
<span style='color:#008000; '>0x7F6A0DBB</span><span style='color:#808030; '>,</span> <span style='color:#008000; '>0x086D3D2D</span><span style='color:#808030; '>,</span> <span style='color:#008000; '>0x91646C97</span><span style='color:#808030; '>,</span> <span style='color:#008000; '>0xE6635C01</span><span style='color:#808030; '>,</span> 
<span style='color:#008000; '>0x6B6B51F4</span><span style='color:#808030; '>,</span> <span style='color:#008000; '>0x1C6C6162</span><span style='color:#808030; '>,</span> <span style='color:#008000; '>0x856530D8</span><span style='color:#808030; '>,</span> <span style='color:#008000; '>0xF262004E</span><span style='color:#808030; '>,</span> 
<span style='color:#008000; '>0x6C0695ED</span><span style='color:#808030; '>,</span> <span style='color:#008000; '>0x1B01A57B</span><span style='color:#808030; '>,</span> <span style='color:#008000; '>0x8208F4C1</span><span style='color:#808030; '>,</span> <span style='color:#008000; '>0xF50FC457</span><span style='color:#808030; '>,</span> 
<span style='color:#008000; '>0x65B0D9C6</span><span style='color:#808030; '>,</span> <span style='color:#008000; '>0x12B7E950</span><span style='color:#808030; '>,</span> <span style='color:#008000; '>0x8BBEB8EA</span><span style='color:#808030; '>,</span> <span style='color:#008000; '>0xFCB9887C</span><span style='color:#808030; '>,</span> 
<span style='color:#008000; '>0x62DD1DDF</span><span style='color:#808030; '>,</span> <span style='color:#008000; '>0x15DA2D49</span><span style='color:#808030; '>,</span> <span style='color:#008000; '>0x8CD37CF3</span><span style='color:#808030; '>,</span> <span style='color:#008000; '>0xFBD44C65</span><span style='color:#808030; '>,</span> 
<span style='color:#008000; '>0x4DB26158</span><span style='color:#808030; '>,</span> <span style='color:#008000; '>0x3AB551CE</span><span style='color:#808030; '>,</span> <span style='color:#008000; '>0xA3BC0074</span><span style='color:#808030; '>,</span> <span style='color:#008000; '>0xD4BB30E2</span><span style='color:#808030; '>,</span> 
<span style='color:#008000; '>0x4ADFA541</span><span style='color:#808030; '>,</span> <span style='color:#008000; '>0x3DD895D7</span><span style='color:#808030; '>,</span> <span style='color:#008000; '>0xA4D1C46D</span><span style='color:#808030; '>,</span> <span style='color:#008000; '>0xD3D6F4FB</span><span style='color:#808030; '>,</span> 
<span style='color:#008000; '>0x4369E96A</span><span style='color:#808030; '>,</span> <span style='color:#008000; '>0x346ED9FC</span><span style='color:#808030; '>,</span> <span style='color:#008000; '>0xAD678846</span><span style='color:#808030; '>,</span> <span style='color:#008000; '>0xDA60B8D0</span><span style='color:#808030; '>,</span> 
<span style='color:#008000; '>0x44042D73</span><span style='color:#808030; '>,</span> <span style='color:#008000; '>0x33031DE5</span><span style='color:#808030; '>,</span> <span style='color:#008000; '>0xAA0A4C5F</span><span style='color:#808030; '>,</span> <span style='color:#008000; '>0xDD0D7CC9</span><span style='color:#808030; '>,</span> 
<span style='color:#008000; '>0x5005713C</span><span style='color:#808030; '>,</span> <span style='color:#008000; '>0x270241AA</span><span style='color:#808030; '>,</span> <span style='color:#008000; '>0xBE0B1010</span><span style='color:#808030; '>,</span> <span style='color:#008000; '>0xC90C2086</span><span style='color:#808030; '>,</span> 
<span style='color:#008000; '>0x5768B525</span><span style='color:#808030; '>,</span> <span style='color:#008000; '>0x206F85B3</span><span style='color:#808030; '>,</span> <span style='color:#008000; '>0xB966D409</span><span style='color:#808030; '>,</span> <span style='color:#008000; '>0xCE61E49F</span><span style='color:#808030; '>,</span> 
<span style='color:#008000; '>0x5EDEF90E</span><span style='color:#808030; '>,</span> <span style='color:#008000; '>0x29D9C998</span><span style='color:#808030; '>,</span> <span style='color:#008000; '>0xB0D09822</span><span style='color:#808030; '>,</span> <span style='color:#008000; '>0xC7D7A8B4</span><span style='color:#808030; '>,</span> 
<span style='color:#008000; '>0x59B33D17</span><span style='color:#808030; '>,</span> <span style='color:#008000; '>0x2EB40D81</span><span style='color:#808030; '>,</span> <span style='color:#008000; '>0xB7BD5C3B</span><span style='color:#808030; '>,</span> <span style='color:#008000; '>0xC0BA6CAD</span><span style='color:#808030; '>,</span> 
 
<span style='color:#008000; '>0xEDB88320</span><span style='color:#808030; '>,</span> <span style='color:#008000; '>0x9ABFB3B6</span><span style='color:#808030; '>,</span> <span style='color:#008000; '>0x03B6E20C</span><span style='color:#808030; '>,</span> <span style='color:#008000; '>0x74B1D29A</span><span style='color:#808030; '>,</span> 
<span style='color:#008000; '>0xEAD54739</span><span style='color:#808030; '>,</span> <span style='color:#008000; '>0x9DD277AF</span><span style='color:#808030; '>,</span> <span style='color:#008000; '>0x04DB2615</span><span style='color:#808030; '>,</span> <span style='color:#008000; '>0x73DC1683</span><span style='color:#808030; '>,</span> 
<span style='color:#008000; '>0xE3630B12</span><span style='color:#808030; '>,</span> <span style='color:#008000; '>0x94643B84</span><span style='color:#808030; '>,</span> <span style='color:#008000; '>0x0D6D6A3E</span><span style='color:#808030; '>,</span> <span style='color:#008000; '>0x7A6A5AA8</span><span style='color:#808030; '>,</span> 
<span style='color:#008000; '>0xE40ECF0B</span><span style='color:#808030; '>,</span> <span style='color:#008000; '>0x9309FF9D</span><span style='color:#808030; '>,</span> <span style='color:#008000; '>0x0A00AE27</span><span style='color:#808030; '>,</span> <span style='color:#008000; '>0x7D079EB1</span><span style='color:#808030; '>,</span> 
<span style='color:#008000; '>0xF00F9344</span><span style='color:#808030; '>,</span> <span style='color:#008000; '>0x8708A3D2</span><span style='color:#808030; '>,</span> <span style='color:#008000; '>0x1E01F268</span><span style='color:#808030; '>,</span> <span style='color:#008000; '>0x6906C2FE</span><span style='color:#808030; '>,</span> 
<span style='color:#008000; '>0xF762575D</span><span style='color:#808030; '>,</span> <span style='color:#008000; '>0x806567CB</span><span style='color:#808030; '>,</span> <span style='color:#008000; '>0x196C3671</span><span style='color:#808030; '>,</span> <span style='color:#008000; '>0x6E6B06E7</span><span style='color:#808030; '>,</span> 
<span style='color:#008000; '>0xFED41B76</span><span style='color:#808030; '>,</span> <span style='color:#008000; '>0x89D32BE0</span><span style='color:#808030; '>,</span> <span style='color:#008000; '>0x10DA7A5A</span><span style='color:#808030; '>,</span> <span style='color:#008000; '>0x67DD4ACC</span><span style='color:#808030; '>,</span> 
<span style='color:#008000; '>0xF9B9DF6F</span><span style='color:#808030; '>,</span> <span style='color:#008000; '>0x8EBEEFF9</span><span style='color:#808030; '>,</span> <span style='color:#008000; '>0x17B7BE43</span><span style='color:#808030; '>,</span> <span style='color:#008000; '>0x60B08ED5</span><span style='color:#808030; '>,</span> 
<span style='color:#008000; '>0xD6D6A3E8</span><span style='color:#808030; '>,</span> <span style='color:#008000; '>0xA1D1937E</span><span style='color:#808030; '>,</span> <span style='color:#008000; '>0x38D8C2C4</span><span style='color:#808030; '>,</span> <span style='color:#008000; '>0x4FDFF252</span><span style='color:#808030; '>,</span> 
<span style='color:#008000; '>0xD1BB67F1</span><span style='color:#808030; '>,</span> <span style='color:#008000; '>0xA6BC5767</span><span style='color:#808030; '>,</span> <span style='color:#008000; '>0x3FB506DD</span><span style='color:#808030; '>,</span> <span style='color:#008000; '>0x48B2364B</span><span style='color:#808030; '>,</span> 
<span style='color:#008000; '>0xD80D2BDA</span><span style='color:#808030; '>,</span> <span style='color:#008000; '>0xAF0A1B4C</span><span style='color:#808030; '>,</span> <span style='color:#008000; '>0x36034AF6</span><span style='color:#808030; '>,</span> <span style='color:#008000; '>0x41047A60</span><span style='color:#808030; '>,</span> 
<span style='color:#008000; '>0xDF60EFC3</span><span style='color:#808030; '>,</span> <span style='color:#008000; '>0xA867DF55</span><span style='color:#808030; '>,</span> <span style='color:#008000; '>0x316E8EEF</span><span style='color:#808030; '>,</span> <span style='color:#008000; '>0x4669BE79</span><span style='color:#808030; '>,</span> 
<span style='color:#008000; '>0xCB61B38C</span><span style='color:#808030; '>,</span> <span style='color:#008000; '>0xBC66831A</span><span style='color:#808030; '>,</span> <span style='color:#008000; '>0x256FD2A0</span><span style='color:#808030; '>,</span> <span style='color:#008000; '>0x5268E236</span><span style='color:#808030; '>,</span> 
<span style='color:#008000; '>0xCC0C7795</span><span style='color:#808030; '>,</span> <span style='color:#008000; '>0xBB0B4703</span><span style='color:#808030; '>,</span> <span style='color:#008000; '>0x220216B9</span><span style='color:#808030; '>,</span> <span style='color:#008000; '>0x5505262F</span><span style='color:#808030; '>,</span> 
<span style='color:#008000; '>0xC5BA3BBE</span><span style='color:#808030; '>,</span> <span style='color:#008000; '>0xB2BD0B28</span><span style='color:#808030; '>,</span> <span style='color:#008000; '>0x2BB45A92</span><span style='color:#808030; '>,</span> <span style='color:#008000; '>0x5CB36A04</span><span style='color:#808030; '>,</span> 
<span style='color:#008000; '>0xC2D7FFA7</span><span style='color:#808030; '>,</span> <span style='color:#008000; '>0xB5D0CF31</span><span style='color:#808030; '>,</span> <span style='color:#008000; '>0x2CD99E8B</span><span style='color:#808030; '>,</span> <span style='color:#008000; '>0x5BDEAE1D</span><span style='color:#808030; '>,</span> 
 
<span style='color:#008000; '>0x9B64C2B0</span><span style='color:#808030; '>,</span> <span style='color:#008000; '>0xEC63F226</span><span style='color:#808030; '>,</span> <span style='color:#008000; '>0x756AA39C</span><span style='color:#808030; '>,</span> <span style='color:#008000; '>0x026D930A</span><span style='color:#808030; '>,</span> 
<span style='color:#008000; '>0x9C0906A9</span><span style='color:#808030; '>,</span> <span style='color:#008000; '>0xEB0E363F</span><span style='color:#808030; '>,</span> <span style='color:#008000; '>0x72076785</span><span style='color:#808030; '>,</span> <span style='color:#008000; '>0x05005713</span><span style='color:#808030; '>,</span> 
<span style='color:#008000; '>0x95BF4A82</span><span style='color:#808030; '>,</span> <span style='color:#008000; '>0xE2B87A14</span><span style='color:#808030; '>,</span> <span style='color:#008000; '>0x7BB12BAE</span><span style='color:#808030; '>,</span> <span style='color:#008000; '>0x0CB61B38</span><span style='color:#808030; '>,</span> 
<span style='color:#008000; '>0x92D28E9B</span><span style='color:#808030; '>,</span> <span style='color:#008000; '>0xE5D5BE0D</span><span style='color:#808030; '>,</span> <span style='color:#008000; '>0x7CDCEFB7</span><span style='color:#808030; '>,</span> <span style='color:#008000; '>0x0BDBDF21</span><span style='color:#808030; '>,</span> 
<span style='color:#008000; '>0x86D3D2D4</span><span style='color:#808030; '>,</span> <span style='color:#008000; '>0xF1D4E242</span><span style='color:#808030; '>,</span> <span style='color:#008000; '>0x68DDB3F8</span><span style='color:#808030; '>,</span> <span style='color:#008000; '>0x1FDA836E</span><span style='color:#808030; '>,</span> 
<span style='color:#008000; '>0x81BE16CD</span><span style='color:#808030; '>,</span> <span style='color:#008000; '>0xF6B9265B</span><span style='color:#808030; '>,</span> <span style='color:#008000; '>0x6FB077E1</span><span style='color:#808030; '>,</span> <span style='color:#008000; '>0x18B74777</span><span style='color:#808030; '>,</span> 
<span style='color:#008000; '>0x88085AE6</span><span style='color:#808030; '>,</span> <span style='color:#008000; '>0xFF0F6A70</span><span style='color:#808030; '>,</span> <span style='color:#008000; '>0x66063BCA</span><span style='color:#808030; '>,</span> <span style='color:#008000; '>0x11010B5C</span><span style='color:#808030; '>,</span> 
<span style='color:#008000; '>0x8F659EFF</span><span style='color:#808030; '>,</span> <span style='color:#008000; '>0xF862AE69</span><span style='color:#808030; '>,</span> <span style='color:#008000; '>0x616BFFD3</span><span style='color:#808030; '>,</span> <span style='color:#008000; '>0x166CCF45</span><span style='color:#808030; '>,</span> 
<span style='color:#008000; '>0xA00AE278</span><span style='color:#808030; '>,</span> <span style='color:#008000; '>0xD70DD2EE</span><span style='color:#808030; '>,</span> <span style='color:#008000; '>0x4E048354</span><span style='color:#808030; '>,</span> <span style='color:#008000; '>0x3903B3C2</span><span style='color:#808030; '>,</span> 
<span style='color:#008000; '>0xA7672661</span><span style='color:#808030; '>,</span> <span style='color:#008000; '>0xD06016F7</span><span style='color:#808030; '>,</span> <span style='color:#008000; '>0x4969474D</span><span style='color:#808030; '>,</span> <span style='color:#008000; '>0x3E6E77DB</span><span style='color:#808030; '>,</span> 
<span style='color:#008000; '>0xAED16A4A</span><span style='color:#808030; '>,</span> <span style='color:#008000; '>0xD9D65ADC</span><span style='color:#808030; '>,</span> <span style='color:#008000; '>0x40DF0B66</span><span style='color:#808030; '>,</span> <span style='color:#008000; '>0x37D83BF0</span><span style='color:#808030; '>,</span> 
<span style='color:#008000; '>0xA9BCAE53</span><span style='color:#808030; '>,</span> <span style='color:#008000; '>0xDEBB9EC5</span><span style='color:#808030; '>,</span> <span style='color:#008000; '>0x47B2CF7F</span><span style='color:#808030; '>,</span> <span style='color:#008000; '>0x30B5FFE9</span><span style='color:#808030; '>,</span> 
<span style='color:#008000; '>0xBDBDF21C</span><span style='color:#808030; '>,</span> <span style='color:#008000; '>0xCABAC28A</span><span style='color:#808030; '>,</span> <span style='color:#008000; '>0x53B39330</span><span style='color:#808030; '>,</span> <span style='color:#008000; '>0x24B4A3A6</span><span style='color:#808030; '>,</span> 
<span style='color:#008000; '>0xBAD03605</span><span style='color:#808030; '>,</span> <span style='color:#008000; '>0xCDD70693</span><span style='color:#808030; '>,</span> <span style='color:#008000; '>0x54DE5729</span><span style='color:#808030; '>,</span> <span style='color:#008000; '>0x23D967BF</span><span style='color:#808030; '>,</span> 
<span style='color:#008000; '>0xB3667A2E</span><span style='color:#808030; '>,</span> <span style='color:#008000; '>0xC4614AB8</span><span style='color:#808030; '>,</span> <span style='color:#008000; '>0x5D681B02</span><span style='color:#808030; '>,</span> <span style='color:#008000; '>0x2A6F2B94</span><span style='color:#808030; '>,</span> 
<span style='color:#008000; '>0xB40BBE37</span><span style='color:#808030; '>,</span> <span style='color:#008000; '>0xC30C8EA1</span><span style='color:#808030; '>,</span> <span style='color:#008000; '>0x5A05DF1B</span><span style='color:#808030; '>,</span> <span style='color:#008000; '>0x2D02EF8D</span><span style='color:#800080; '>}</span><span style='color:#800080; '>;</span>

        readonly <span style='color:#800000; font-weight:bold; '>static</span> Encoding encoder <span style='color:#808030; '>=</span> Encoding<span style='color:#808030; '>.</span>GetEncoding<span style='color:#808030; '>(</span><span style='color:#008c00; '>1252</span><span style='color:#808030; '>)</span><span style='color:#800080; '>;</span>
        readonly <span style='color:#800000; font-weight:bold; '>static</span> ulong poly <span style='color:#808030; '>=</span> <span style='color:#008c00; '>4294967295</span><span style='color:#800080; '>;</span>

        <span style='color:#3f5fbf; '>/// &lt;summary> </span>
        <span style='color:#3f5fbf; '>/// Get the crc32 value for an entire Stream, setting the position to zero. </span>
        <span style='color:#3f5fbf; '>/// &lt;/summary> </span>
        <span style='color:#3f5fbf; '>/// &lt;param name="st">The stream to perform the crc32 calculation on.&lt;/param> </span>
        <span style='color:#3f5fbf; '>/// &lt;returns>The crc32 value.&lt;/returns> </span>
        public <span style='color:#800000; font-weight:bold; '>long</span> CRC<span style='color:#808030; '>(</span>Stream st<span style='color:#808030; '>)</span>
        <span style='color:#800080; '>{</span>
            <span style='color:#800000; font-weight:bold; '>return</span> CRC<span style='color:#808030; '>(</span>st<span style='color:#808030; '>,</span> <span style='color:#008c00; '>0</span><span style='color:#808030; '>,</span> st<span style='color:#808030; '>.</span>Length<span style='color:#808030; '>)</span><span style='color:#800080; '>;</span>
        <span style='color:#800080; '>}</span>

        <span style='color:#3f5fbf; '>/// &lt;summary> </span>
        <span style='color:#3f5fbf; '>/// Get the crc32 value for a Stream, setting the position to to the beginPosition and calculation to the length. </span>
        <span style='color:#3f5fbf; '>/// The position is set back to the original position when complete. </span>
        <span style='color:#3f5fbf; '>/// &lt;/summary> </span>
        <span style='color:#3f5fbf; '>/// &lt;param name="st">The stream to perform the crc32 calculation on.&lt;/param> </span>
        <span style='color:#3f5fbf; '>/// &lt;param name="beginPosition">The begin position of the stream to start the calculation.&lt;/param> </span>
        <span style='color:#3f5fbf; '>/// &lt;param name="length">The length you wish to run the calculation on.&lt;/param> </span>
        <span style='color:#3f5fbf; '>/// &lt;returns>The crc32 value.&lt;/returns> </span>
        public <span style='color:#800000; font-weight:bold; '>long</span> CRC<span style='color:#808030; '>(</span>Stream st<span style='color:#808030; '>,</span> <span style='color:#800000; font-weight:bold; '>long</span> beginPosition<span style='color:#808030; '>,</span> <span style='color:#800000; font-weight:bold; '>long</span> length<span style='color:#808030; '>)</span>
        <span style='color:#800080; '>{</span>
            ulong ulCRC <span style='color:#808030; '>=</span> poly<span style='color:#800080; '>;</span>
            <span style='color:#800000; font-weight:bold; '>long</span> originalPos <span style='color:#808030; '>=</span> st<span style='color:#808030; '>.</span>Position<span style='color:#800080; '>;</span>
            <span style='color:#800000; font-weight:bold; '>long</span> endPos <span style='color:#808030; '>=</span> beginPosition <span style='color:#808030; '>+</span> length<span style='color:#800080; '>;</span>
            byte by<span style='color:#800080; '>;</span>

            <span style='color:#800000; font-weight:bold; '>if</span> <span style='color:#808030; '>(</span>endPos <span style='color:#808030; '>></span> st<span style='color:#808030; '>.</span>Length<span style='color:#808030; '>)</span>
            <span style='color:#800080; '>{</span>
                throw new Exception<span style='color:#808030; '>(</span><span style='color:#800000; '>"</span><span style='color:#0000e6; '>Out of bounds. beginposition + length is greater than the length of the Stream</span><span style='color:#800000; '>"</span><span style='color:#808030; '>)</span><span style='color:#800080; '>;</span>
            <span style='color:#800080; '>}</span>

            try
            <span style='color:#800080; '>{</span>
                st<span style='color:#808030; '>.</span>Position <span style='color:#808030; '>=</span> beginPosition<span style='color:#800080; '>;</span>
                BufferedStream bs <span style='color:#808030; '>=</span> new BufferedStream<span style='color:#808030; '>(</span>st<span style='color:#808030; '>)</span><span style='color:#800080; '>;</span>

                <span style='color:#800000; font-weight:bold; '>for</span> <span style='color:#808030; '>(</span><span style='color:#800000; font-weight:bold; '>long</span> i <span style='color:#808030; '>=</span> beginPosition<span style='color:#800080; '>;</span> i <span style='color:#808030; '>&lt;</span> endPos<span style='color:#800080; '>;</span> i<span style='color:#808030; '>+</span><span style='color:#808030; '>+</span><span style='color:#808030; '>)</span>
                <span style='color:#800080; '>{</span>
                    by <span style='color:#808030; '>=</span> Convert<span style='color:#808030; '>.</span>ToByte<span style='color:#808030; '>(</span>bs<span style='color:#808030; '>.</span>ReadByte<span style='color:#808030; '>(</span><span style='color:#808030; '>)</span><span style='color:#808030; '>)</span><span style='color:#800080; '>;</span>
                    ulCRC <span style='color:#808030; '>=</span> <span style='color:#808030; '>(</span>ulCRC <span style='color:#808030; '>></span><span style='color:#808030; '>></span> <span style='color:#008c00; '>8</span><span style='color:#808030; '>)</span> <span style='color:#808030; '>^</span> crcLookup<span style='color:#808030; '>[</span><span style='color:#808030; '>(</span>ulCRC <span style='color:#808030; '>&amp;</span> <span style='color:#008000; '>0xFF</span><span style='color:#808030; '>)</span> <span style='color:#808030; '>^</span> by<span style='color:#808030; '>]</span><span style='color:#800080; '>;</span>
                <span style='color:#800080; '>}</span>
            <span style='color:#800080; '>}</span>
            catch <span style='color:#808030; '>(</span>Exception e<span style='color:#808030; '>)</span>
            <span style='color:#800080; '>{</span>
                Console<span style='color:#808030; '>.</span>WriteLine<span style='color:#808030; '>(</span>e<span style='color:#808030; '>.</span>ToString<span style='color:#808030; '>(</span><span style='color:#808030; '>)</span><span style='color:#808030; '>)</span><span style='color:#800080; '>;</span>
            <span style='color:#800080; '>}</span>
            <span style='color:#800000; font-weight:bold; '>finally</span>
            <span style='color:#800080; '>{</span>
                <span style='color:#696969; '>//For now do nothing </span>
            <span style='color:#800080; '>}</span>
            st<span style='color:#808030; '>.</span>Position <span style='color:#808030; '>=</span> originalPos<span style='color:#800080; '>;</span>
            <span style='color:#800000; font-weight:bold; '>return</span> Convert<span style='color:#808030; '>.</span>ToInt64<span style='color:#808030; '>(</span>ulCRC <span style='color:#808030; '>^</span> poly<span style='color:#808030; '>)</span><span style='color:#800080; '>;</span>
        <span style='color:#800080; '>}</span>

        <span style='color:#3f5fbf; '>/// &lt;summary> </span>
        <span style='color:#3f5fbf; '>/// Get the crc32 value for a String. </span>
        <span style='color:#3f5fbf; '>/// &lt;/summary> </span>
        <span style='color:#3f5fbf; '>/// &lt;param name="text">The string you wish to calculate the crc32 value on.&lt;/param> </span>
        <span style='color:#3f5fbf; '>/// &lt;returns>The CRC-32 value.&lt;/returns> </span>
        public <span style='color:#800000; font-weight:bold; '>long</span> CRC<span style='color:#808030; '>(</span>string text<span style='color:#808030; '>)</span>
        <span style='color:#800080; '>{</span>
            byte<span style='color:#808030; '>[</span><span style='color:#808030; '>]</span> buffer<span style='color:#800080; '>;</span>
            buffer <span style='color:#808030; '>=</span> encoder<span style='color:#808030; '>.</span>GetBytes<span style='color:#808030; '>(</span>text<span style='color:#808030; '>)</span><span style='color:#800080; '>;</span>
            <span style='color:#800000; font-weight:bold; '>return</span> CRC<span style='color:#808030; '>(</span>buffer<span style='color:#808030; '>)</span><span style='color:#800080; '>;</span>
        <span style='color:#800080; '>}</span>

        <span style='color:#3f5fbf; '>/// &lt;summary> </span>
        <span style='color:#3f5fbf; '>/// Get the CRC-32 value for a byte[]. </span>
        <span style='color:#3f5fbf; '>/// &lt;/summary> </span>
        <span style='color:#3f5fbf; '>/// &lt;param name="by">The byte[] you wish to calculate the crc32 value on&lt;/param> </span>
        <span style='color:#3f5fbf; '>/// &lt;returns>The CRC-32 value.&lt;/returns> </span>
        public <span style='color:#800000; font-weight:bold; '>long</span> CRC<span style='color:#808030; '>(</span>byte<span style='color:#808030; '>[</span><span style='color:#808030; '>]</span> by<span style='color:#808030; '>)</span>
        <span style='color:#800080; '>{</span>
            ulong ulCRC <span style='color:#808030; '>=</span> poly<span style='color:#800080; '>;</span>
            <span style='color:#800000; font-weight:bold; '>long</span> len<span style='color:#800080; '>;</span>
            len <span style='color:#808030; '>=</span> by<span style='color:#808030; '>.</span>Length<span style='color:#800080; '>;</span>
            <span style='color:#800000; font-weight:bold; '>for</span> <span style='color:#808030; '>(</span><span style='color:#800000; font-weight:bold; '>long</span> i <span style='color:#808030; '>=</span> <span style='color:#008c00; '>0</span><span style='color:#800080; '>;</span> i <span style='color:#808030; '>&lt;</span> len<span style='color:#800080; '>;</span> i<span style='color:#808030; '>+</span><span style='color:#808030; '>+</span><span style='color:#808030; '>)</span>
            <span style='color:#800080; '>{</span>
                ulCRC <span style='color:#808030; '>=</span> <span style='color:#808030; '>(</span>ulCRC <span style='color:#808030; '>></span><span style='color:#808030; '>></span> <span style='color:#008c00; '>8</span><span style='color:#808030; '>)</span> <span style='color:#808030; '>^</span> crcLookup<span style='color:#808030; '>[</span><span style='color:#808030; '>(</span>ulCRC <span style='color:#808030; '>&amp;</span> <span style='color:#008000; '>0xFF</span><span style='color:#808030; '>)</span> <span style='color:#808030; '>^</span> by<span style='color:#808030; '>[</span>i<span style='color:#808030; '>]</span><span style='color:#808030; '>]</span><span style='color:#800080; '>;</span>
            <span style='color:#800080; '>}</span>
            <span style='color:#800000; font-weight:bold; '>return</span> Convert<span style='color:#808030; '>.</span>ToInt64<span style='color:#808030; '>(</span>ulCRC <span style='color:#808030; '>^</span> poly<span style='color:#808030; '>)</span><span style='color:#800080; '>;</span>
        <span style='color:#800080; '>}</span>
    <span style='color:#800080; '>}</span>
<span style='color:#800080; '>}</span>
</pre>
<!--Created using ToHtml.com on 2021-12-29 13:50:11 UTC -->