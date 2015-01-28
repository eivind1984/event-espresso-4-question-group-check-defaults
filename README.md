# event-espresso-4-question-group-check-defaults
I needed to have question groups automatically checked in the add new event-screen. No feature was available, so I made this jquery thing that does the trick.

Use at own risk, but this might be a nice starting point, at least :)

## Step 1: Add this to your functions.php:

´´´
add_action('admin_footer', 'my_custom_check_eventcheckboxes');

function my_custom_check_eventcheckboxes() {
    $screen = get_current_screen();
    if ( $screen->id != "espresso_events" )   // Only add it to event espresso related pages
        return;

?>

    <script type="text/javascript">
        jQuery(document).ready(function($) {
                $("#espresso_events_Registration_Form_Hooks_Extend_additional_questions_metabox #event-question-group-3 :checkbox").prop('checked', true);
                $("#espresso_events_Registration_Form_Hooks_Extend_primary_questions_metabox #event-question-group-2 :checkbox").prop('checked', true);
                $("#espresso_events_Registration_Form_Hooks_Extend_primary_questions_metabox #event-question-group-4 :checkbox").prop('checked', true);
                $( "[name='externalURL']" ).parent().css( "display", "none" );
        });
    </script>

<?php
}
´´´

Step 2: Change it to fit your needs

The above code will check question group 3 for additional attendees, and groups 2 and for for the primary attendee. You may of course remove some of them or add more if you need.

In order to make it check the question groups you want to, inspect your output HTML code for the add new event page, and find the id of the p containing the question group you'd like to check.

For instance, this is the output HTML for question group 3, and you can see the id belongs to the p element:

´´´
<p id="event-question-group-3">
						<input value="3" type="checkbox" name="question_groups[3]" />
						<a href="http://domainname.no/wp-admin/admin.php?page=espresso_registration_form&action=edit_question_group&QSG_ID=3&edit_question_group_nonce=93e05e1167&return=edit" title="Edit question group" target="_blank">Barn</a>
					</p>
´´´


