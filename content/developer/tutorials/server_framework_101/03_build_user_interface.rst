===================================
Chapter 3: Build the user interface
===================================

In this chapter, we will bring our application to life by building a :abbr:`UI (User Interface)`
that allows users to interact with the models. This will require defining menu items, actions, and
views. By the end of this chapter, we will have a fully functional interface to manage real estate
properties!

.. _tutorials/server_framework_101/menu_items:

Add menus items
===============

**Menus items** are the first thing users see and interact with. They give users access to the
different parts of Odoo and can be nested to form a hierarchical structure. This allows the
functionalities of complex applications to be organized into categories and sub-categories and makes
them easier to navigate. The top level of the menu structure typically contains the menu items for
the main applications (like "Contacts", "Sales", and "Accounting"). These top-level menu items can
also be visually enhanced with custom icons for better recognition.

Menu items can take on two distinct roles:

- **Category menu items**: They serve as organizational containers and simply expand to show their
  submenu when clicked.
- **Action menu items**: They trigger a specific action in the UI when clicked. While menu items
  often trigger actions, they are separate entities. The same action can be triggered by different
  menu items, or even buttons.

In Odoo, menu items are actually records of the `ir.ui.menu` model whose key fields are:

.. rst-class:: o-definition-list

`name` (required)
   The title of the menu item.
`sequence`
   Determines the ordering of same-level menu items.
`parent_id`
   The ID of the parent menu item's record.
`web_icon`
   The path to the icon file to use as a menu item icon.
`action`
   The action to trigger when the menu item is clicked.

Like for any other model, one can automatically create records of the `ir.ui.menu` model by means of
a data file. Let’s do just that and add menu items to our real estate app!

.. exercise::
   #. Create and declare a new :file:`menus.xml` file at the root of the `real_estate` module.
   #. Describe a new "Real Estate" menu item to serve as root menu for our real estate app.

      - Leave the `parent_id` field empty to place the menu item in the top-level menu.
      - Use the `static/description/icon.png` file as `web_icon`, in the format
        `<module>,<icon_file_path>`.

   #. Nest new "Properties" and "Settings" menu items under the root menu item. As we have not yet
      created an action to browse properties or open settings, reference the following existing
      actions instead:

      - `base.open_module_tree` that opens the list of modules.
      - `base.action_client_base_menu` that opens the general settings.

.. spoiler:: Solution

   .. code-block:: python
      :caption: `__manifest__.py`
      :emphasize-lines: 3

      'data': [
          'ir.model.access.csv',
          'menus.xml',
          'real_estate_property_data.xml',
      ],

   .. code-block:: xml
      :caption: `menus.xml`

      <?xml version="1.0"?>
      <odoo>

          <record id="real_estate.root_menu" model="ir.ui.menu">
              <field name="name">Real Estate</field>
              <field name="web_icon">real_estate,static/description/icon.png</field>
          </record>

          <record id="real_estate.properties_menu" model="ir.ui.menu">
              <field name="name">Properties</field>
              <field name="sequence">10</field>
              <field name="parent_id" ref="real_estate.root_menu"/>
              <field name="action" ref="base.open_module_tree"/>
          </record>

          <record id="real_estate.settings_menu" model="ir.ui.menu">
              <field name="name">Settings</field>
              <field name="sequence">20</field>
              <field name="parent_id" ref="real_estate.root_menu"/>
              <field name="action" ref="base.action_client_base_menu"/>
          </record>

      </odoo>

If you go to the app switcher :dfn:`the top-level menu of Odoo`, you should now see a menu item for
our real estate app! Click it to open the app and automatically trigger the first action in its
sub-menu. If you referenced the `base.open_module_tree` action, you should now see a list of Odoo
modules.

Use the `menuitem` shortcut
---------------------------

As an application grows in size, so do its menus, and it becomes increasingly complicated to define
and nest menu items. While defining menu items using the `record` data operation works perfectly
fine, the server framework provides a shortcut that makes the process easier and more intuitive,
especially for nesting menu items: the `menuitem` data operation.

The `menuitem` tag is a special XML element that is specifically designed for creating menu items;
it simplifies the syntax and automatically handles some technical details for you.

.. example::
   Our fictional `product` module could define menu items as follows:

   .. code-block:: xml

      <menuitem id="product.root_menu" name="Product" web_icon="product,static/description/product.png">
          <menuitem id="product.products_menu" name="Products" sequence="10" action="product.view_products_action"/>
      </menuitem>

   .. note::
      - The outer `menuitem` element creates the top-level "Product" menu item.
      - The specifications (`name`, `web_icon`, `sequence`, `action`, ...) of menu items are set
        through attributes of the XML element.
      - The menu items hierarchy is defined by nesting their XML elements.

Why keep complex code when you can simplify it? It's already time for our first **code
refactoring**!

.. exercise::
   Rewrite the description of the menu items of our real estate app using the `menuitem` data
   operation instead of `record`.

.. spoiler:: Solution

   .. code-block:: xml
      :caption: `menus.xml`
      :emphasize-lines: 4-21

      <?xml version="1.0"?>
      <odoo>

          <menuitem
              id="real_estate.root_menu"
              name="Real Estate"
              web_icon="real_estate,static/description/icon.png"
          >
              <menuitem
                  id="real_estate.properties_menu"
                  name="Properties"
                  sequence="10"
                  action="base.open_module_tree"
              />
              <menuitem
                  id="real_estate.settings_menu"
                  name="Settings"
                  sequence="20"
                  action="base.action_client_base_menu"
              />
          </menuitem>

      </odoo>

.. _tutorials/server_framework_101/define_actions:

Define actions
==============

**Actions** define what happens when a user interacts with the UI, such as clicking a menu item.
They connect the user interface with the underlying business logic. There exist different types of
actions in Odoo, the most common one being **window actions** (`ir.actions.act_window`), that
display the records of a specific model in a view. Other types of actions allow for different
behaviors, like **URL actions** that open URLs (`ir.actions.act_url`) or **server actions**
(`ir.actions.server`) that execute custom code.

In Odoo, actions can be stored in the database as records or returned as Python dictionaries
interpreted as action descriptors when business logic is executed. Window actions are described by
the `ir.actions.act_window` model whose key fields include:

.. rst-class:: o-definition-list

`name` (required)
   The title of the action; is often used as the page title.
`res_model` (required)
   The model on which the action operates.
`view_mode`
   A comma-separated list of view types to enable for this action; for example, `tree,form,kanban`.
`help`
   An optional help text for the users when there are no records to display.

.. seealso::
   :doc:`Reference documentation for actions <../../reference/backend/actions>`

.. example::
   The example below defines an action to open existing products in either tree or form view.

   .. code-block:: xml

      <record id="product.view_products_action" model="ir.actions.act_window">
          <field name="name">Products</field>
          <field name="res_model">product</field>
          <field name="view_mode">tree,form</field>
          <field name="help" type="html">
              <p class="o_view_nocontent_smiling_face">
                  Create a new product.
              </p>
          </field>
      </record>

   .. note::
      The content of the `help` field can be written in different formats thanks to the `type`
      attribute of the :ref:`field <reference/data/field>` data operation.

As promised, we'll finally get to interact with our real estate properties in the UI. All we need
now is an action to assign to the menu item.

.. exercise::

   #. Create and declare a new :file:`actions.xml` file at the root of the `real_estate` module.

      .. tip::
         Pay attention to the declaration order of data files in the manifest; you might introduce a
         data operation that depends on another one.

   #. Describe a new "Properties" action that opens `real.estate.property` records in tree and form
      views, and assign it to the "Properties" menu item. Be creative with the help text! For
      reference, the list of supported classes can be found in the `view.scss
      <{GITHUB_PATH}/addons/web/static/src/views/view.scss>`_ file.

.. spoiler:: Solution

   .. code-block:: python
      :caption: `__manifest__.py`
      :emphasize-lines: 2,4

      'data': [
          'actions.xml',
          'ir.model.access.csv',
          'menus.xml',  # Depends on `actions.xml`
          'real_estate_property_data.xml',
      ],

   .. code-block:: xml
      :caption: `actions.xml`

      <?xml version="1.0"?>
      <odoo>

          <record id="real_estate.views_properties_action" model="ir.actions.act_window">
              <field name="name">Properties</field>
              <field name="res_model">real.estate.property</field>
              <field name="view_mode">tree,form</field>
              <field name="help" type="html">
                  <!-- Turns out I didn't feel like being creative with the help text ¯\_(ツ)_/¯ -->
                  <p class="o_view_nocontent_smiling_face">
                      Create a new property.
                  </p>
              </field>
          </record>

      </odoo>

   .. code-block:: xml
      :caption: `menus.xml`
      :emphasize-lines: 5

      <menuitem
          id="real_estate.properties_menu"
          name="Properties"
          sequence="10"
          action="real_estate.views_properties_action"
      />

Clicking the "Properties" menu item now displays a tree view of the default properties we created
earlier. As we specified in the action that both tree and form views were allowed, you can click any
property record to display its form view. Delete all three records to see the help text you created.

.. _tutorials/server_framework_101/create_views:

Create views
============

**Views** are the UI's building blocks, defining how model data is displayed on screen. They are
structures written in XML that describe the layout and behavior of various UI components.

Odoo supports different types of views, each serving a different purpose. The most common types
include **tree views** for listing multiple records in a table-like format, **form views** for
displaying and editing individual records, **kanban views** for presenting records in a card layout,
and **search views** for defining search and filtering options.

.. note::
   For historical reasons, list views are called tree views in Odoo.

In Odoo, views are records of the `ir.ui.view` model. Key fields include:

.. rst-class:: o-definition-list

`name` (required)
   A unique name for the view.
`model` (required)
   The model the view is associated with.
`arch` (required)
   The view architecture as an XML string.

.. seealso::
   TODO
   .. :doc:`Reference documentation for views <../../reference/backend/actions>`

.. todo:: comment examples

.. example::
   .. code-block:: xml

      <record id="product_list" model="ir.ui.view">
          <field name="name">product.list</field>
          <field name="model">product</field>
          <field name="arch" type="xml">
              <tree>
                  <field name="name"/>
                  <field name="price"/>
                  <field name="category"/>
              </tree>
          </field>
      </record>

   .. code-block:: xml

      <record id="product_form" model="ir.ui.view">
          <field name="name">product.form</field>
          <field name="model">product</field>
          <field name="arch" type="xml">
              <form>
                  <sheet>
                      <group>
                          <field name="name"/>
                          <field name="description"/>
                          <field name="price"/>
                          <field name="category"/>
                      </group>
                  </sheet>
              </form>
          </field>
      </record>

.. todo:: If you deleted the default property records earlier, restart the server to load them again.
.. todo:: link to https://odoo.com/documentation/developer/reference/user_interface/view_records.html
.. todo:: link to https://odoo.com/documentation/developer/reference/user_interface/view_architectures.html
.. todo:: add exercise to create a list view of the real_estate_property model
.. todo:: add exercise to create a form view of the real_estate_property model
.. todo:: add the solution

----

.. todo: add incentive for chapter 4
