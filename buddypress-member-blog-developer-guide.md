# Plugin/Theme Developer Guide for buddypress-member-blog

## Table of Contents

- [`\admin\class-buddypress-member-blog-admin.php`](#\admin\class-buddypress-member-blog-admin.php)
- [`\admin\inc\bp-member-blog-setting-general-tab.php`](#\admin\inc\bp-member-blog-setting-general-tab.php)
- [`\includes\buddypress-member-blog-functions.php`](#\includes\buddypress-member-blog-functions.php)
- [`\includes\class-buddypress-member-blog.php`](#\includes\class-buddypress-member-blog.php)
- [`\public\class-buddypress-member-blog-public.php`](#\public\class-buddypress-member-blog-public.php)
- [`\templates\draft-posts.php`](#\templates\draft-posts.php)
- [`\templates\edit.php`](#\templates\edit.php)
- [`\templates\pending-posts.php`](#\templates\pending-posts.php)
- [`\templates\posts.php`](#\templates\posts.php)

## do_action Hooks in `\admin\class-buddypress-member-blog-admin.php`

### Hook: `bp_member_blog_tab_contents`
- **Type:** do_action
- **File:** `\admin\class-buddypress-member-blog-admin.php`
- **Line:** 216

## apply_filters Hooks in `\admin\class-buddypress-member-blog-admin.php`

### Hook: `bp_member_blog_admin_setting_tabs`
- **Type:** apply_filters
- **File:** `\admin\class-buddypress-member-blog-admin.php`
- **Line:** 147

## do_action Hooks in `\admin\inc\bp-member-blog-setting-general-tab.php`

### Hook: `bp_member_blog_add_general_settings_options`
- **Type:** do_action
- **File:** `\admin\inc\bp-member-blog-setting-general-tab.php`
- **Line:** 207

## apply_filters Hooks in `\includes\buddypress-member-blog-functions.php`

### Hook: `bp_member_change_blog_slug`
- **Type:** apply_filters
- **File:** `\includes\buddypress-member-blog-functions.php`
- **Line:** 256

### Hook: `default_content`
- **Type:** apply_filters
- **File:** `\includes\buddypress-member-blog-functions.php`
- **Line:** 347

### Hook: `default_title`
- **Type:** apply_filters
- **File:** `\includes\buddypress-member-blog-functions.php`
- **Line:** 355

### Hook: `default_excerpt`
- **Type:** apply_filters
- **File:** `\includes\buddypress-member-blog-functions.php`
- **Line:** 363

### Hook: `bp_member_blog_template_dir`
- **Type:** apply_filters
- **File:** `\includes\buddypress-member-blog-functions.php`
- **Line:** 430

## Shortcodes in `\includes\class-buddypress-member-blog.php`

### Shortcode: `bp-member-blog`
- **Callback Function:** `$plugin_public,`
- **File:** `\includes\class-buddypress-member-blog.php`
- **Line:** 196

## do_action Hooks in `\public\class-buddypress-member-blog-public.php`

### Hook: `buddypress_member_blog_post_save`
- **Type:** do_action
- **File:** `\public\class-buddypress-member-blog-public.php`
- **Line:** 570

### Hook: `buddypress_member_blog_post_submit`
- **Type:** do_action
- **File:** `\public\class-buddypress-member-blog-public.php`
- **Line:** 674

## apply_filters Hooks in `\public\class-buddypress-member-blog-public.php`

### Hook: `bp_member_change_blog_label`
- **Type:** apply_filters
- **File:** `\public\class-buddypress-member-blog-public.php`
- **Line:** 186

### Hook: `bp_member_change_blog_slug`
- **Type:** apply_filters
- **File:** `\public\class-buddypress-member-blog-public.php`
- **Line:** 187

### Hook: `bp_member_change_blog_label`
- **Type:** apply_filters
- **File:** `\public\class-buddypress-member-blog-public.php`
- **Line:** 222

### Hook: `bp_member_change_blog_slug`
- **Type:** apply_filters
- **File:** `\public\class-buddypress-member-blog-public.php`
- **Line:** 223

### Hook: `bp_member_change_blog_label`
- **Type:** apply_filters
- **File:** `\public\class-buddypress-member-blog-public.php`
- **Line:** 244

### Hook: `bp_member_change_blog_slug`
- **Type:** apply_filters
- **File:** `\public\class-buddypress-member-blog-public.php`
- **Line:** 245

### Hook: `bp_member_change_blog_label`
- **Type:** apply_filters
- **File:** `\public\class-buddypress-member-blog-public.php`
- **Line:** 318

### Hook: `bp_member_change_blog_slug`
- **Type:** apply_filters
- **File:** `\public\class-buddypress-member-blog-public.php`
- **Line:** 319

## do_action Hooks in `\templates\draft-posts.php`

### Hook: `bp_member_blog_before_posts`
- **Type:** do_action
- **File:** `\templates\draft-posts.php`
- **Line:** 57

## do_action Hooks in `\templates\edit.php`

### Hook: `bp_post_before_title`
- **Type:** do_action
- **File:** `\templates\edit.php`
- **Line:** 61

### Hook: `bp_post_after_title`
- **Type:** do_action
- **File:** `\templates\edit.php`
- **Line:** 68

### Hook: `bp_post_after_content`
- **Type:** do_action
- **File:** `\templates\edit.php`
- **Line:** 71

### Hook: `bp_post_after_content`
- **Type:** do_action
- **File:** `\templates\edit.php`
- **Line:** 89

### Hook: `bp_post_before_category`
- **Type:** do_action
- **File:** `\templates\edit.php`
- **Line:** 93

### Hook: `bp_post_after_category`
- **Type:** do_action
- **File:** `\templates\edit.php`
- **Line:** 156

### Hook: `bp_post_before_tag`
- **Type:** do_action
- **File:** `\templates\edit.php`
- **Line:** 158

### Hook: `bp_post_after_tag`
- **Type:** do_action
- **File:** `\templates\edit.php`
- **Line:** 179

### Hook: `bp_post_before_featured_image`
- **Type:** do_action
- **File:** `\templates\edit.php`
- **Line:** 182

### Hook: `bp_post_after_featured_image`
- **Type:** do_action
- **File:** `\templates\edit.php`
- **Line:** 199

### Hook: `bp_post_before_submit_button`
- **Type:** do_action
- **File:** `\templates\edit.php`
- **Line:** 209

## apply_filters Hooks in `\templates\edit.php`

### Hook: `bp_member_blog_terms_args`
- **Type:** apply_filters
- **File:** `\templates\edit.php`
- **Line:** 47

### Hook: `bp_member_blog_post_content`
- **Type:** apply_filters
- **File:** `\templates\edit.php`
- **Line:** 79

## do_action Hooks in `\templates\pending-posts.php`

### Hook: `bp_member_blog_before_posts`
- **Type:** do_action
- **File:** `\templates\pending-posts.php`
- **Line:** 59

## do_action Hooks in `\templates\posts.php`

### Hook: `bp_member_blog_before_posts`
- **Type:** do_action
- **File:** `\templates\posts.php`
- **Line:** 56

