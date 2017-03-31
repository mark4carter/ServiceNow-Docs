UI Pages
====================================================

Triggering on change for select box
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

To prevent using gel, we can pass in the current value of the select box using `this.value`

HTML
------

    .. code-block:: html

        <g:evaluate>
          var choiceList = new GlideChoiceList();
          choiceList.add('', '--None--');
          choiceList.add('123', 'OneTwoThree');
          choiceList.add('FourFiveSix', '456');
        </g:evaluate>
        
        <select id="document_select" name="document_select" onchange="myFunction(this.value)">
          <g:options choiceList="${choiceList}" choiceValue="" />
        </select>

Client Script
-----------------

  .. code-block:: javascript

    function myFunction(val) {
      alert(val);
    }


Using a passed parameter in HTML field
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

HTML
----------

  .. code-block:: html

    <g:evaluate var="jvar_document_array"
    expression="RP.getWindowProperties().get('sysparm_document_array')" />
  
    <script>
      alert('"${jvar_document_array}"');
    </script>



Using a passed parameter in the Client field
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Client script
------------------

  .. code-block:: html

    alert('"${sysparm_document_array}"');