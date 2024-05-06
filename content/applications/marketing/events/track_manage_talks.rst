============================
Talks, proposals, and agenda
============================

With Odoo *Events*, users can utilize a fully-integrated event website, where attendees can quickly
access various tracks (talks, presentations, etc.), view entire agendas, and propose talks for the
event.

Event website
=============

To access an event website, navigate to the specific event form in the Odoo *Events* app, and click
the :guilabel:`Go to Website` smart button. Or, while on the Odoo-built website for the company,
click the :guilabel:`Events` header option, and select the desired event to view that event's
website.

On the event website, there is an event-specific subheader menu with different options to choose
from.

With the *Schedule & Tracks* setting enabled in the Odoo *Events* app, the following links are
automatically added to the subheader menu, located on the event website: :guilabel:`Talks`,
:guilabel:`Talk Proposals`, and :guilabel:`Agenda`.

.. image:: track_manage_talks/track-submenu-options.png
   :align: center
   :alt: The track-related event submenu options on an event website built with Odoo Events.

To enable the :guilabel:`Schedule & Tracks` setting, navigate to :menuselection:`Events app -->
Configuration --> Settings`, tick the checkbox beside :guilabel:`Schedule & Tracks`, and click
:guilabel:`Save`.

Talks page
----------

The :guilabel:`Talks` link takes the attendee to a page filled with all the planned tracks for the
event.

.. image:: track_manage_talks/talks-page.png
   :align: center
   :alt: The Talks page on an event website built through the Odoo Events application.

At the top of :guilabel:`Talks` page, there are drop-down filter menus beside a :guilabel:`Search
a talk...` search bar.

The first drop-down filter menu (with the starting title: :guilabel:`Favorites`) is the only
drop-down filter menu that appears by default. When clicked, the resulting menu presents two
options: :guilabel:`Favorites` and :guilabel:`All Talks`.

Selecting :guilabel:`Favorites` shows *only* the tracks that have been favorited by the attendee.

.. note::
   If no tracks have been favorited, and the :guilabel:`Favorites` filter is selected, Odoo presents
   all the event tracks.

Selecting :guilabel:`All Talks` shows *all* the tracks, regardless if they have been favorited or
not.

The other drop-down filter menus that appear on this page are related to any configured tags (and
tag categories) created for event tracks in the backend.

.. tip::
   To add tags and tag categories to track forms, open a desired event track form, and start typing
   a new tag in the :guilabel:`Tags` field. Then, click :guilabel:`Create and edit...` from the
   resulting drop-down menu.

   Doing so reveals a :guilabel:`Create Tags` pop-up form.

   .. image:: track_manage_talks/create-tags-popup.png
      :align: center
      :alt: The Create Tags pop-up form that coincides with drop-down filter menus on Talks page.

   From here, users see the recently added tag in the :guilabel:`Tag Name` field. Beneath that,
   there is an option to add a specific :guilabel:`Color Index` to the tag for added organization.

   Lastly, there is the :guilabel:`Category` field, where users can either select a pre-existing
   category for this new tag, or create a new one.

   All options in the :guilabel:`Category` field for tags appear as their own drop-down filter menu
   on the :guilabel:`Talks` page, located on the event website.

Beneath the drop-down filter menus at the top of the :guilabel:`Talks` page, there is a list of
planned tracks for the specific event, organized by day.

If an attendee wishes to favorite a track, they can click the :icon:`fa-bell-o` :guilabel:`(empty
bell)` icon, located to the right of the track title. Attendees will know a track has been favorited
when they notice the icon has been changed to :icon:`fa-bell` :guilabel:`(filled bell)` icon.

Favoriting a track this way places it on the list of :guilabel:`Favorites`, which is accessible from
the default drop-down filter menu, located at the top of the :guilabel:`Talks` page.

Talk Proposals page
-------------------

The :guilabel:`Talk Proposals` link takes attendees to a page on the event website, wherein they can
formerly submit a proposal for a talk (:dfn:`track`) for the event, via a custom online form.

.. image:: track_manage_talks/talk-proposals-page.png
   :align: center
   :alt: The Talk Proposals page on the event website built with the Odoo Events application.

In addition to the form, an introduction to the page, along with any other pertinent information
related to the types of talks the event will feature can be added, if needed.

The talk proposal form can be modified in a number of different ways, via the web builder tools,
accessible by clicking :guilabel:`Edit` while on the specific page.

Then, proceed to edit any of the default fields, or add new forms with the :guilabel:`Form` building
block (located in the :guilabel:`Blocks` section of the web builder tools sidebar).

Once all the necessary information is entered into the form, the attendees just need to click the
:guilabel:`Submit Proposal` button.

Then, that talk, and all the information entered on the form, can be accessed on the
:guilabel:`Event Tracks` page for that specific event in the :guilabel:`Proposal` stage, which is
accessible via the :guilabel:`Tracks` smart button on the event form.

At that point, an internal user can review the proposed talk, and choose to accept or deny the
proposal.

If accepted, the internal user can then move the track to the next appropriate stage in the Kanban
pipeline on the :guilabel:`Event Tracks` page for the event. Then, they can open that track form,
and click the :guilabel:`Go to Website` smart button to reveal that track's page on the event
website.

From there, they can toggle the :guilabel:`Unpublished` switch in the header to
:guilabel:`Published`, which allows all event attendees to view and access the talk.

Agenda page
-----------

The :guilabel:`Agenda` link takes attendees to a page on the event website, showcasing an event
calendar, depicting when (and where) events are taking place for that specific event.

.. image:: track_manage_talks/event-agenda-page.png
   :align: center
   :alt: The event Agenda page on the event website built with the Odoo Events application.

Clicking any track on the calendar takes the attendee to that specific track's detail page on the
event website.

<<<<<<< HEAD
In the upper right corner, toggle the switch from :guilabel:`Unpublished` to :guilabel:`Published`,
and the talk is instantly accessible on the website.

.. note::
   Without publishing a talk, attendees will never be able to access it.

.. image:: track_manage_talks/events-tracks-publish.png
   :align: center
   :alt: View of the website page to publish a proposed talk for Odoo Events.

Attendees list and attendance
-----------------------------

Once attendees have registered for a specific event, they are added to the :guilabel:`Attendee List`
for that event, which is accessible via the :guilabel:`Attendees` smart button on the event template
form, or :menuselection:`Reporting --> Attendees` and sorted by event.

.. note::
   When an attendee arrives at the event, they will be marked as attending (:guilabel:`Confirmed
   Attendance`), and the status of that attendee will change to :guilabel:`Attended.`

.. image:: track_manage_talks/events-attendees-smartbutton.png
   :align: center
   :alt: Overview of events with the kanban view in Odoo Events.

When analyzing an :guilabel:`Attendees list`, Odoo provides different ways to view the information.
Each view option presents the same information, but in a slightly different layout. To change the
view, click on the icons in the upper right hand of the screen.

.. image:: track_manage_talks/events-attendees-view-options.png
   :align: center
   :alt: Various view options on the attendees list page.

In the :guilabel:`Kanban` view, it can be confirmed whether the attendees have already paid or
remain unpaid.

The :guilabel:`List` view provides information in a more traditional list formation.

The :guilabel:`Calendar` view provides a clear schedule visualization of which attendees are
arriving on specific dates of the event.

The :guilabel:`Graph` view provides graphical representations of that event's attendees, along with
numerous filters and customizable measures for deeper analysis.

The :guilabel:`Cohort` view lays out attendee data to better analyze the number of registration
dates.

.. note::
   Tickets sold through sales orders validate attendees as soon as the quotation is confirmed.

Manage registrations
--------------------

Upon selecting an attendee, Odoo reveals that specific attendee's detail form.

From here, event badges can be sent manually, by selecting :guilabel:`Send By Email`. The
:guilabel:`Attendee` can also be marked as :guilabel:`Attended`, or the registration can be
cancelled altogether via the :guilabel:`Cancel Registration` button.

.. image:: track_manage_talks/events-send-email-button.png
   :align: center
   :alt: View of an attendee form emphasizing the send by email and cancel registration in Odoo
         Events.

Lead Generation Rules
---------------------

With Odoo, leads can be generated from events.

To create and configure a :guilabel:`Lead Generation Rule` related to events, navigate to
:menuselection:`Events app --> Configuration --> Lead Generation`.

On the :guilabel:`Lead Generation Rule` page, every configured :guilabel:`Lead Generation Rule`
can be found, along with pertinent data related to those rules.

.. image:: track_manage_talks/events-lead-generation-rule-page.png
   :align: center
   :alt: How the Lead Generation Rule page looks in Odoo Events.

To create a new :guilabel:`Lead Generation Rule`, click :guilabel:`Create`, and fill out the
:guilabel:`Lead Generation Rule` form.

.. image:: track_manage_talks/events-lead-generation-rule-template.png
   :align: center
   :alt: How the Lead Generation Rule template looks in Odoo Events.

After naming the rule, configure *how* the lead should be created (either :guilabel:`Per Attendee`
or :guilabel:`Per Order`), and *when* they should be created, (when
:guilabel:`Attendees are created`, when :guilabel:`Attendees are confirmed`, or when
:guilabel:`Attendees attended` the event).

In the :guilabel:`For any of these Events` section, there are fields to attach this rule to any
specific event categories, company, and/or event. To add even more specificity to the rule, a
domain filter rule can be configured to ensure the rule only applies to a specific target audience
of attendees (found in the :guilabel:`If the Attendees meet these Conditions` section).

Lastly, in the :guilabel:`Lead Default Values` section, designate a :guilabel:`Lead Type`, then
assign it to a specific :guilabel:`Sales Team` (and/or :guilabel:`Salesperson`), and attach tags to
the rule, if necessary.
||||||| parent of 28586978e (temp)
In the upper right corner, toggle the switch from :guilabel:`Unpublished` to :guilabel:`Published`,
and the talk is instantly accessible on the website.

.. note::
   Without publishing a talk, attendees will never be able to access it.

.. image:: track_manage_talks/events-tracks-publish.png
   :align: center
   :alt: View of the website page to publish a proposed talk for Odoo Events.

Attendees list and attendance
-----------------------------

Once attendees have registered for a specific event, they are added to the :guilabel:`Attendee List`
for that event, which is accessible via the :guilabel:`Attendees` smart button on the event template
form, or :menuselection:`Reporting --> Attendees` and sorted by event.

.. note::
   When an attendee arrives at the event, they will be marked as attending (:guilabel:`Confirmed
   Attendance`), and the status of that attendee will change to :guilabel:`Attended.`

.. image:: track_manage_talks/events-attendees-smartbutton.png
   :align: center
   :alt: Overview of events with the kanban view in Odoo Events.

When analyzing an :guilabel:`Attendees list`, Odoo provides different ways to view the information.
Each view option presents the same information, but in a slightly different layout. To change the
view, click on the icons in the upper right hand of the screen.

.. image:: track_manage_talks/events-attendees-view-options.png
   :align: center
   :alt: Various view options on the attendees list page.

In the :guilabel:`Kanban` view, it can be confirmed whether the attendees have already paid or
remain unpaid.

The :guilabel:`List` view provides information in a more traditional list formation.

The :guilabel:`Calendar` view provides a clear schedule visualization of which attendees are
arriving on specific dates of the event.

The :guilabel:`Graph` view provides graphical representations of that event's attendees, along with
numerous filters and customizable measures for deeper analysis.

The :guilabel:`Cohort` view lays out attendee data to better analyze the number of registration
dates.

.. note::
   Tickets sold through sales orders validate attendees as soon as the quotation is confirmed.

Manage registrations
--------------------

Upon selecting an attendee, Odoo reveals that specific attendee's detail form.

From here, event badges can be sent manually, by selecting :guilabel:`Send By Email`. The
:guilabel:`Attendee` can also be marked as :guilabel:`Attended`, or the registration can be
canceled altogether via the :guilabel:`Cancel Registration` button.

.. image:: track_manage_talks/events-send-email-button.png
   :align: center
   :alt: View of an attendee form emphasizing the send by email and cancel registration in Odoo
         Events.

Lead Generation Rules
---------------------

With Odoo, leads can be generated from events.

To create and configure a :guilabel:`Lead Generation Rule` related to events, navigate to
:menuselection:`Events app --> Configuration --> Lead Generation`.

On the :guilabel:`Lead Generation Rule` page, every configured :guilabel:`Lead Generation Rule`
can be found, along with pertinent data related to those rules.

.. image:: track_manage_talks/events-lead-generation-rule-page.png
   :align: center
   :alt: How the Lead Generation Rule page looks in Odoo Events.

To create a new :guilabel:`Lead Generation Rule`, click :guilabel:`Create`, and fill out the
:guilabel:`Lead Generation Rule` form.

.. image:: track_manage_talks/events-lead-generation-rule-template.png
   :align: center
   :alt: How the Lead Generation Rule template looks in Odoo Events.

After naming the rule, configure *how* the lead should be created (either :guilabel:`Per Attendee`
or :guilabel:`Per Order`), and *when* they should be created, (when
:guilabel:`Attendees are created`, when :guilabel:`Attendees are confirmed`, or when
:guilabel:`Attendees attended` the event).

In the :guilabel:`For any of these Events` section, there are fields to attach this rule to any
specific event categories, company, and/or event. To add even more specificity to the rule, a
domain filter rule can be configured to ensure the rule only applies to a specific target audience
of attendees (found in the :guilabel:`If the Attendees meet these Conditions` section).

Lastly, in the :guilabel:`Lead Default Values` section, designate a :guilabel:`Lead Type`, then
assign it to a specific :guilabel:`Sales Team` (and/or :guilabel:`Salesperson`), and attach tags to
the rule, if necessary.
=======
If an attendee wishes to favorite a track, they can click the :icon:`fa-bell-o` :guilabel:`(empty
bell)` icon, located to the right of the track title. Attendees will know a track has been favorited
when they notice the icon has been changed to :icon:`fa-bell` :guilabel:`(filled bell)` icon.
>>>>>>> 28586978e (temp)
