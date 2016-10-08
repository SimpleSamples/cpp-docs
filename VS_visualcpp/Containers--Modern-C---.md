---
title: "Containers (Modern C++)"
ms.custom: na
ms.date: 10/03/2016
ms.devlang: 
  - C++
ms.prod: visual-studio-dev14
ms.reviewer: na
ms.suite: na
ms.technology: 
  - devlang-cpp
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 6e10b758-e928-4827-9c3f-86cafe54bf5b
caps.latest.revision: 7
manager: ghogen
translation.priority.ht: 
  - de-de
  - es-es
  - fr-fr
  - it-it
  - ja-jp
  - ko-kr
  - ru-ru
  - zh-cn
  - zh-tw
translation.priority.mt: 
  - cs-cz
  - pl-pl
  - pt-br
  - tr-tr
---
# Containers (Modern C++)
<?xml version="1.0" encoding="utf-8"?>
<developerConceptualDocument xmlns="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="http://ddue.schemas.microsoft.com/authoring/2003/5 http://clixdevr3.blob.core.windows.net/ddueschema/developer.xsd">
  <introduction>
    <para>By default, use <legacyLink xlink:href="a3e0a8f8-7565-4fe0-93e4-e4d74ae1b70d">vector</legacyLink> as the default sequential container in C++. This is the equivalent of List&lt;T&gt; in other languages. </para>
    <code language="cpp">vector&lt;string&gt; v;
v.push_back( "Geddy Lee" );
</code>
    <para>Use <legacyLink xlink:href="7876f4c9-ebb4-4878-af1e-09364c43af0a">map</legacyLink> (not unordered_map) as the default associative container. Use <legacyLink xlink:href="8991f9aa-5509-4440-adc1-371512d32018">set</legacyLink>, <legacyLink xlink:href="8796ae05-37c4-475a-9e61-75fde9d4a463">multimap</legacyLink>, <legacyLink xlink:href="630e8c10-0ce9-4ad9-8d79-9e91a600713f">multiset</legacyLink> for degenerate &amp; multi cases.</para>
    <code language="cpp">map&lt;string, string&gt; phone_book;
// ...
phone_book["Alex Lifeson"] = "+1 (416) 555-1212";
</code>
    <para>When performance optimization is needed, consider using: </para>
    <list class="ordered">
      <listItem>
        <para>the array type when embedding is important - for example, as a class member.</para>
      </listItem>
      <listItem>
        <para>unordered associative containers (unordered_map, et al.): Lower per-element overhead (major) and constant-time lookup (potentially major, sometimes minor). Harder to use correctly and efficiently, because of inconveniences and sharp edges.</para>
      </listItem>
      <listItem>
        <para>sorted vector. (See: <legacyLink xlink:href="6f758d3c-a7c7-4a50-92bb-97b2f6d4ab27">Algorithms</legacyLink>.)</para>
      </listItem>
    </list>
    <para>Don’t use C arrays. (For older APIs, use <codeInline>f( vec.data(), vec.size() );</codeInline> .)</para>
    <para>For another article about containers, see <link xlink:href="8e915ca1-19ba-4f0d-93c8-e2c3bfd638eb">STL Containers</link>.</para>
  </introduction>
  <section>
    <title>Container Sizes</title>
    <content>
      <para>The following tables show the container sizes, in bytes, for x86 and x64 platforms.  (For these purposes, 32-bit ARM is equivalent to x86.)  These tables cover release mode, because debug mode contains checking machinery that consumes space and time.  The separate columns are for <token>cpp_orcas_long</token> SP1, where <codeInline>_SECURE_SCL</codeInline> defaulted to 1, and for <token>cpp_orcas_long</token> SP1 with <codeInline>_SECURE_SCL</codeInline> manually set to 0 for maximum speed.  Visual C++ in Visual Studio 2010, <token>cpp_dev11_long</token>, and <token>cpp_dev12_long</token> default <codeInline>_SECURE_SCL</codeInline> to 0 (now known as <codeInline>_ITERATOR_DEBUG_LEVEL</codeInline>).</para>
      <table xmlns:caps="http://schemas.microsoft.com/build/caps/2013/11">
        <thead>
          <tr>
            <TD>
              <para>x86 Container Sizes (Bytes)</para>
            </TD>
            <TD>
              <para>VC9 SP1</para>
            </TD>
            <TD>
              <para>VC9 SP1  </para>
              <para>SCL=0</para>
            </TD>
            <TD>
              <para>VC10</para>
            </TD>
            <TD>
              <para>VC11</para>
            </TD>
          </tr>
        </thead>
        <tbody>
          <tr>
            <TD>
              <para>vector&lt;int&gt;</para>
            </TD>
            <TD>
              <para>24</para>
            </TD>
            <TD>
              <para>16</para>
            </TD>
            <TD>
              <para>16</para>
            </TD>
            <TD>
              <para>12</para>
            </TD>
          </tr>
          <tr>
            <TD>
              <para>array&lt;int, 5&gt;</para>
            </TD>
            <TD>
              <para>20</para>
            </TD>
            <TD>
              <para>20</para>
            </TD>
            <TD>
              <para>20</para>
            </TD>
            <TD>
              <para>20</para>
            </TD>
          </tr>
          <tr>
            <TD>
              <para>deque&lt;int&gt;</para>
            </TD>
            <TD>
              <para>32</para>
            </TD>
            <TD>
              <para>32</para>
            </TD>
            <TD>
              <para>24</para>
            </TD>
            <TD>
              <para>20</para>
            </TD>
          </tr>
          <tr>
            <TD>
              <para>forward_list&lt;int&gt;</para>
            </TD>
            <TD>
              <para>N/A</para>
            </TD>
            <TD>
              <para>N/A</para>
            </TD>
            <TD>
              <para>8</para>
            </TD>
            <TD>
              <para>4</para>
            </TD>
          </tr>
          <tr>
            <TD>
              <para>list&lt;int&gt;</para>
            </TD>
            <TD>
              <para>28</para>
            </TD>
            <TD>
              <para>12</para>
            </TD>
            <TD>
              <para>12</para>
            </TD>
            <TD>
              <para>8</para>
            </TD>
          </tr>
          <tr>
            <TD>
              <para>priority_queue&lt;int&gt;</para>
            </TD>
            <TD>
              <para>28</para>
            </TD>
            <TD>
              <para>20</para>
            </TD>
            <TD>
              <para>20</para>
            </TD>
            <TD>
              <para>16</para>
            </TD>
          </tr>
          <tr>
            <TD>
              <para>queue&lt;int&gt;</para>
            </TD>
            <TD>
              <para>32</para>
            </TD>
            <TD>
              <para>32</para>
            </TD>
            <TD>
              <para>24</para>
            </TD>
            <TD>
              <para>20</para>
            </TD>
          </tr>
          <tr>
            <TD>
              <para>stack&lt;int&gt;</para>
            </TD>
            <TD>
              <para>32</para>
            </TD>
            <TD>
              <para>32</para>
            </TD>
            <TD>
              <para>24</para>
            </TD>
            <TD>
              <para>20</para>
            </TD>
          </tr>
          <tr>
            <TD>
              <para>pair&lt;int, int&gt;</para>
            </TD>
            <TD>
              <para>8</para>
            </TD>
            <TD>
              <para>8</para>
            </TD>
            <TD>
              <para>8</para>
            </TD>
            <TD>
              <para>8</para>
            </TD>
          </tr>
          <tr>
            <TD>
              <para>tuple&lt;int, int, int&gt;</para>
            </TD>
            <TD>
              <para>16</para>
            </TD>
            <TD>
              <para>16</para>
            </TD>
            <TD>
              <para>16</para>
            </TD>
            <TD>
              <para>12</para>
            </TD>
          </tr>
          <tr>
            <TD>
              <para>map&lt;int, int&gt;</para>
            </TD>
            <TD>
              <para>32</para>
            </TD>
            <TD>
              <para>12</para>
            </TD>
            <TD>
              <para>16</para>
            </TD>
            <TD>
              <para>8</para>
            </TD>
          </tr>
          <tr>
            <TD>
              <para>multimap&lt;int, int&gt;</para>
            </TD>
            <TD>
              <para>32</para>
            </TD>
            <TD>
              <para>12</para>
            </TD>
            <TD>
              <para>16</para>
            </TD>
            <TD>
              <para>8</para>
            </TD>
          </tr>
          <tr>
            <TD>
              <para>set&lt;int&gt;</para>
            </TD>
            <TD>
              <para>32</para>
            </TD>
            <TD>
              <para>12</para>
            </TD>
            <TD>
              <para>16</para>
            </TD>
            <TD>
              <para>8</para>
            </TD>
          </tr>
          <tr>
            <TD>
              <para>multiset&lt;int&gt;</para>
            </TD>
            <TD>
              <para>32</para>
            </TD>
            <TD>
              <para>12</para>
            </TD>
            <TD>
              <para>16</para>
            </TD>
            <TD>
              <para>8</para>
            </TD>
          </tr>
          <tr>
            <TD>
              <para>hash_map&lt;int, int&gt;</para>
            </TD>
            <TD>
              <para>72</para>
            </TD>
            <TD>
              <para>44</para>
            </TD>
            <TD>
              <para>44</para>
            </TD>
            <TD>
              <para>32</para>
            </TD>
          </tr>
          <tr>
            <TD>
              <para>hash_multimap&lt;int, int&gt;</para>
            </TD>
            <TD>
              <para>72</para>
            </TD>
            <TD>
              <para>44</para>
            </TD>
            <TD>
              <para>44</para>
            </TD>
            <TD>
              <para>32</para>
            </TD>
          </tr>
          <tr>
            <TD>
              <para>hash_set&lt;int&gt;</para>
            </TD>
            <TD>
              <para>72</para>
            </TD>
            <TD>
              <para>44</para>
            </TD>
            <TD>
              <para>44</para>
            </TD>
            <TD>
              <para>32</para>
            </TD>
          </tr>
          <tr>
            <TD>
              <para>hash_multiset&lt;int&gt;</para>
            </TD>
            <TD>
              <para>72</para>
            </TD>
            <TD>
              <para>44</para>
            </TD>
            <TD>
              <para>44</para>
            </TD>
            <TD>
              <para>32</para>
            </TD>
          </tr>
          <tr>
            <TD>
              <para>unordered_map&lt;int, int&gt;</para>
            </TD>
            <TD>
              <para>72</para>
            </TD>
            <TD>
              <para>44</para>
            </TD>
            <TD>
              <para>44</para>
            </TD>
            <TD>
              <para>32</para>
            </TD>
          </tr>
          <tr>
            <TD>
              <para>unordered_multimap&lt;int, int&gt;</para>
            </TD>
            <TD>
              <para>72</para>
            </TD>
            <TD>
              <para>44</para>
            </TD>
            <TD>
              <para>44</para>
            </TD>
            <TD>
              <para>32</para>
            </TD>
          </tr>
          <tr>
            <TD>
              <para>unordered_set&lt;int&gt;</para>
            </TD>
            <TD>
              <para>72</para>
            </TD>
            <TD>
              <para>44</para>
            </TD>
            <TD>
              <para>44</para>
            </TD>
            <TD>
              <para>32</para>
            </TD>
          </tr>
          <tr>
            <TD>
              <para>unordered_multiset&lt;int&gt;</para>
            </TD>
            <TD>
              <para>72</para>
            </TD>
            <TD>
              <para>44</para>
            </TD>
            <TD>
              <para>44</para>
            </TD>
            <TD>
              <para>32</para>
            </TD>
          </tr>
          <tr>
            <TD>
              <para>string</para>
            </TD>
            <TD>
              <para>28</para>
            </TD>
            <TD>
              <para>28</para>
            </TD>
            <TD>
              <para>28</para>
            </TD>
            <TD>
              <para>24</para>
            </TD>
          </tr>
          <tr>
            <TD>
              <para>wstring</para>
            </TD>
            <TD>
              <para>28</para>
            </TD>
            <TD>
              <para>28</para>
            </TD>
            <TD>
              <para>28</para>
            </TD>
            <TD>
              <para>24</para>
            </TD>
          </tr>
        </tbody>
      </table>
      <table xmlns:caps="http://schemas.microsoft.com/build/caps/2013/11">
        <thead>
          <tr>
            <TD>
              <para>x64 Container Sizes (Bytes)</para>
            </TD>
            <TD>
              <para>VC9 SP1</para>
            </TD>
            <TD>
              <para>VC9 SP1 </para>
              <para>SCL=0</para>
            </TD>
            <TD>
              <para>VC10</para>
            </TD>
            <TD>
              <para>VC11</para>
            </TD>
          </tr>
        </thead>
        <tbody>
          <tr>
            <TD>
              <para>vector&lt;int&gt;</para>
            </TD>
            <TD>
              <para>48</para>
            </TD>
            <TD>
              <para>32</para>
            </TD>
            <TD>
              <para>32</para>
            </TD>
            <TD>
              <para>24</para>
            </TD>
          </tr>
          <tr>
            <TD>
              <para>array&lt;int, 5&gt;</para>
            </TD>
            <TD>
              <para>20</para>
            </TD>
            <TD>
              <para>20</para>
            </TD>
            <TD>
              <para>20</para>
            </TD>
            <TD>
              <para>20</para>
            </TD>
          </tr>
          <tr>
            <TD>
              <para>deque&lt;int&gt;</para>
            </TD>
            <TD>
              <para>64</para>
            </TD>
            <TD>
              <para>64</para>
            </TD>
            <TD>
              <para>48</para>
            </TD>
            <TD>
              <para>40</para>
            </TD>
          </tr>
          <tr>
            <TD>
              <para>forward_list&lt;int&gt;</para>
            </TD>
            <TD>
              <para>N/A</para>
            </TD>
            <TD>
              <para>N/A</para>
            </TD>
            <TD>
              <para>16</para>
            </TD>
            <TD>
              <para>8</para>
            </TD>
          </tr>
          <tr>
            <TD>
              <para>list&lt;int&gt;</para>
            </TD>
            <TD>
              <para>56</para>
            </TD>
            <TD>
              <para>24</para>
            </TD>
            <TD>
              <para>24</para>
            </TD>
            <TD>
              <para>16</para>
            </TD>
          </tr>
          <tr>
            <TD>
              <para>priority_queue&lt;int&gt;</para>
            </TD>
            <TD>
              <para>56</para>
            </TD>
            <TD>
              <para>40</para>
            </TD>
            <TD>
              <para>40</para>
            </TD>
            <TD>
              <para>32</para>
            </TD>
          </tr>
          <tr>
            <TD>
              <para>queue&lt;int&gt;</para>
            </TD>
            <TD>
              <para>64</para>
            </TD>
            <TD>
              <para>64</para>
            </TD>
            <TD>
              <para>48</para>
            </TD>
            <TD>
              <para>40</para>
            </TD>
          </tr>
          <tr>
            <TD>
              <para>stack&lt;int&gt;</para>
            </TD>
            <TD>
              <para>64</para>
            </TD>
            <TD>
              <para>64</para>
            </TD>
            <TD>
              <para>48</para>
            </TD>
            <TD>
              <para>40</para>
            </TD>
          </tr>
          <tr>
            <TD>
              <para>pair&lt;int, int&gt;</para>
            </TD>
            <TD>
              <para>8</para>
            </TD>
            <TD>
              <para>8</para>
            </TD>
            <TD>
              <para>8</para>
            </TD>
            <TD>
              <para>8</para>
            </TD>
          </tr>
          <tr>
            <TD>
              <para>tuple&lt;int, int, int&gt;</para>
            </TD>
            <TD>
              <para>16</para>
            </TD>
            <TD>
              <para>16</para>
            </TD>
            <TD>
              <para>16</para>
            </TD>
            <TD>
              <para>12</para>
            </TD>
          </tr>
          <tr>
            <TD>
              <para>map&lt;int, int&gt;</para>
            </TD>
            <TD>
              <para>64</para>
            </TD>
            <TD>
              <para>24</para>
            </TD>
            <TD>
              <para>32</para>
            </TD>
            <TD>
              <para>16</para>
            </TD>
          </tr>
          <tr>
            <TD>
              <para>multimap&lt;int, int&gt;</para>
            </TD>
            <TD>
              <para>64</para>
            </TD>
            <TD>
              <para>24</para>
            </TD>
            <TD>
              <para>32</para>
            </TD>
            <TD>
              <para>16</para>
            </TD>
          </tr>
          <tr>
            <TD>
              <para>set&lt;int&gt;</para>
            </TD>
            <TD>
              <para>64</para>
            </TD>
            <TD>
              <para>24</para>
            </TD>
            <TD>
              <para>32</para>
            </TD>
            <TD>
              <para>16</para>
            </TD>
          </tr>
          <tr>
            <TD>
              <para>multiset&lt;int&gt;</para>
            </TD>
            <TD>
              <para>64</para>
            </TD>
            <TD>
              <para>24</para>
            </TD>
            <TD>
              <para>32</para>
            </TD>
            <TD>
              <para>16</para>
            </TD>
          </tr>
          <tr>
            <TD>
              <para>hash_map&lt;int, int&gt;</para>
            </TD>
            <TD>
              <para>144</para>
            </TD>
            <TD>
              <para>88</para>
            </TD>
            <TD>
              <para>88</para>
            </TD>
            <TD>
              <para>64</para>
            </TD>
          </tr>
          <tr>
            <TD>
              <para>hash_multimap&lt;int, int&gt;</para>
            </TD>
            <TD>
              <para>144</para>
            </TD>
            <TD>
              <para>88</para>
            </TD>
            <TD>
              <para>88</para>
            </TD>
            <TD>
              <para>64</para>
            </TD>
          </tr>
          <tr>
            <TD>
              <para>hash_set&lt;int&gt;</para>
            </TD>
            <TD>
              <para>144</para>
            </TD>
            <TD>
              <para>88</para>
            </TD>
            <TD>
              <para>88</para>
            </TD>
            <TD>
              <para>64</para>
            </TD>
          </tr>
          <tr>
            <TD>
              <para>hash_multiset&lt;int&gt;</para>
            </TD>
            <TD>
              <para>144</para>
            </TD>
            <TD>
              <para>88</para>
            </TD>
            <TD>
              <para>88</para>
            </TD>
            <TD>
              <para>64</para>
            </TD>
          </tr>
          <tr>
            <TD>
              <para>unordered_map&lt;int, int&gt;</para>
            </TD>
            <TD>
              <para>144</para>
            </TD>
            <TD>
              <para>88</para>
            </TD>
            <TD>
              <para>88</para>
            </TD>
            <TD>
              <para>64</para>
            </TD>
          </tr>
          <tr>
            <TD>
              <para>unordered_multimap&lt;int, int&gt;</para>
            </TD>
            <TD>
              <para>144</para>
            </TD>
            <TD>
              <para>88</para>
            </TD>
            <TD>
              <para>88</para>
            </TD>
            <TD>
              <para>64</para>
            </TD>
          </tr>
          <tr>
            <TD>
              <para>unordered_set&lt;int&gt;</para>
            </TD>
            <TD>
              <para>144</para>
            </TD>
            <TD>
              <para>88</para>
            </TD>
            <TD>
              <para>88</para>
            </TD>
            <TD>
              <para>64</para>
            </TD>
          </tr>
          <tr>
            <TD>
              <para>unordered_multiset&lt;int&gt;</para>
            </TD>
            <TD>
              <para>144</para>
            </TD>
            <TD>
              <para>88</para>
            </TD>
            <TD>
              <para>88</para>
            </TD>
            <TD>
              <para>64</para>
            </TD>
          </tr>
          <tr>
            <TD>
              <para>string</para>
            </TD>
            <TD>
              <para>40</para>
            </TD>
            <TD>
              <para>40</para>
            </TD>
            <TD>
              <para>40</para>
            </TD>
            <TD>
              <para>32</para>
            </TD>
          </tr>
          <tr>
            <TD>
              <para>wstring</para>
            </TD>
            <TD>
              <para>40</para>
            </TD>
            <TD>
              <para>40</para>
            </TD>
            <TD>
              <para>40</para>
            </TD>
            <TD>
              <para>32</para>
            </TD>
          </tr>
        </tbody>
      </table>
    </content>
  </section>
  <relatedTopics>
    <link xlink:href="1cb1b849-ed9c-4721-a972-fd8f3dab42e2">Welcome Back to C++</link>
    <link xlink:href="4be9cacb-c862-4391-894a-3a118c9c93ce">C++ Language Reference</link>
    <link xlink:href="a37d3ba3-58af-47c7-9ee2-441ccd7b77ee">Standard C++ Library</link>
  </relatedTopics>
</developerConceptualDocument>